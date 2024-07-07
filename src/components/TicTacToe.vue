<template>
  <div class="tic-tac-toe">
    <h1>Tic Tac Toe</h1>
    <div class="board">
      <div v-for="(cell, index) in board" :key="index" class="cell" @click="makeMove(index)">
        {{ cell }}
      </div>
    </div>
    <div v-if="winner" class="result">
      <p>{{ winner }} wins!</p>
      <button @click="resetGame">Play Again</button>
    </div>
    <div v-else-if="isBoardFull" class="result">
      <p>It's a draw!</p>
      <button @click="resetGame">Play Again</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TicTacToe',
  data() {
    return {
      board: Array(9).fill(null),
      currentPlayer: 'X',
      winner: null
    };
  },
  computed: {
    isBoardFull() {
      return this.board.every(cell => cell !== null);
    }
  },
  methods: {
    makeMove(index) {
      if (!this.board[index] && !this.winner) {
        this.board[index] = this.currentPlayer;
        if (this.checkWinner()) {
          this.winner = this.currentPlayer;
        } else {
          this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
        }
      }
    },
    checkWinner() {
      const winningCombinations = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
      ];
      return winningCombinations.some(combination => {
        const [a, b, c] = combination;
        return this.board[a] && this.board[a] === this.board[b] && this.board[a] === this.board[c];
      });
    },
    resetGame() {
      this.board = Array(9).fill(null);
      this.currentPlayer = 'X';
      this.winner = null;
    }
  }
};
</script>

<style scoped>
.tic-tac-toe {
  text-align: center;
  font-family: Arial, sans-serif;
}

.board {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  grid-gap: 10px;
  margin: 20px auto;
}

.cell {
  width: 100px;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 24px;
  border: 1px solid #333;
  cursor: pointer;
  user-select: none;
}

.cell:hover {
  background-color: #f0f0f0;
}

.result {
  margin-top: 20px;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}
</style>
