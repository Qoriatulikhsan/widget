<template>
  <div class="tic-tac-toe-widget bg-gray-200 border-2 border-gray-900 p-4 mb-4 h-full mt-40 ml-96 mr-96 rounded-lg">
    <h2 class="text-3xl font-bold mb-5 text-gray-900">Tic Tac Toe</h2>
    <div class="board grid grid-cols-3 gap-4 mb-2">
      <div v-for="(cell, index) in board" :key="index" @click="handleClick(index)" class="border border-gray-900 h-12 flex items-center justify-center cursor-pointer">
        {{ cell }}
      </div>
    </div>
    <button @click="resetGame" class=" bg-gray-900 mt-2 py-2 px-4  text-white rounded-full">Reset</button>
    <p class="mt-3 text-xl font-semibold ">{{ status }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      board: ['', '', '', '', '', '', '', '', ''],
      currentPlayer: 'X',
      isGameEnded: false,
    };
  },
  computed: {
    status() {
      if (this.isGameEnded) {
        return 'Game Over!';
      }
      return `Player ${this.currentPlayer}'s turn`;
    },
  },
  methods: {
    handleClick(index) {
      if (!this.isGameEnded && this.board[index] === '') {
        this.board[index] = this.currentPlayer;
        this.checkWinner();
        this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
      }
    },
    checkWinner() {
      const winningCombinations = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8], // Rows
        [0, 3, 6], [1, 4, 7], [2, 5, 8], // Columns
        [0, 4, 8], [2, 4, 6], // Diagonals
      ];

      for (const combination of winningCombinations) {
        const [a, b, c] = combination;
        if (this.board[a] && this.board[a] === this.board[b] && this.board[a] === this.board[c]) {
          this.isGameEnded = true;
          return;
        }
      }
    },
    resetGame() {
      this.board = ['', '', '', '', '', '', '', '', ''];
      this.currentPlayer = 'X';
      this.isGameEnded = false;
    },
  },
};
</script>


