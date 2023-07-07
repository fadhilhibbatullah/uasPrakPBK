<template>
    <div class="tic-tac-toe-widget">
      <h2>Tic Tac Toe</h2>
      <div class="board">
        <div v-for="(cell, index) in board" :key="index" @click="handleClick(index)">{{ cell }}</div>
      </div>
      <button @click="resetGame">Reset</button>
      <p>{{ status }}{{ deskp }}</p>
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
            this.deskp=` Player ${this.currentPlayer} wins!`;
            return;
          }
        }
      },
      resetGame() {
        this.board = ['', '', '', '', '', '', '', '', ''];
        this.currentPlayer = 'X';
        this.isGameEnded = false;
        this.deskp=``;
      },
    },
  };
  </script>
  
  <style scoped>
  .tic-tac-toe-widget {
    display: flex;
    flex-direction: column;
    border: 1px solid rgb(204, 204, 204);
    padding: 20px;
    margin-bottom: 20px;
    align-items: center;
    justify-content: center;
  }
  
  .board {
    background-color: #7853b4;
    display: grid;
    width: 350px;
    height: 350px;
    grid-template-columns: repeat(3, 1fr);
   
    margin-bottom: 10px;
    align-items: center;
    justify-content: center;
    padding: 10px;
    margin-right: 0px;
  }
  
  .board div {
    border: 2px solid #ccc;
    background-color: rgba(18, 0, 179, 0.344);


  

    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;

    font-size: 20px;
  }
  
  button {
    margin-top: 10px;
    background-color: #000000;
    color: white;
    border: none;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s ease;
    font-family: 'poppins';
  }
  button:hover {
    background-color: #ff0202;

  }
  </style>