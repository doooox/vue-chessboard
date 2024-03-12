<template>
    <button 
        class="new-game-btn" 
        @click="resetGame()"
    >
        New Game
    </button>
    <div class="chessboard">
      <div class="board-header">
        <div class="board-header-cell"></div>
        <div
          v-for="col in cols"
          :key="'header-' + col"
          class="board-header-cell"
        >
          {{ col  }}
        </div>
      </div>
      <div 
        v-for="row in rows" 
        :key="'row-' + row" 
        class="board-row"
      >
        <div class="board-header-cell">
          {{ row }}
        </div>
        <div
        v-for="col in cols"
        :key="row + '-' + col"
        :class="{ 'even': (row + cols.indexOf(col)) % 2 === 0, 'selected': isSelected(row, col) }"
        @click="cellClicked(row, col)"
        class="board-cell"
      >
        </div>
      </div>

      <div class="clicked-cells">
        <h4>Cells Clicked:</h4>
        <div 
            v-for="clickedCell in clickedCells" 
            :key="clickedCell"
        >
          {{ clickedCell }}
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        cols : ["A","B","C","D","E","F","G","H"],
        rows : [1,2,3,4,5,6,7,8],
        clickedCells: [],
        selectedCell:null
      };
    },
    methods: {
      cellClicked(row, col) {
        const clickedCell = `${col}${row}`;
        this.clickedCells.push(clickedCell);
        this.selectedCell = clickedCell; 
      },
      isSelected(row, col) {
        const clickedCell = `${col}${row}`;
        return this.selectedCell === clickedCell;
      },
      resetGame(){
        this.clickedCells = [];
        this.selectedCell = null;
      }
    },
  };
  </script>
  
  <style scoped>
    .new-game-btn{
        display: inline-block;
        text-transform: uppercase;
        text-decoration: none;
        padding: 10px 20px;
        border-radius: 30px;
        transition: all 0.3s;
        margin: 20px;
    }
    
    .new-game-btn:hover{
        transform: translateY(-5px);
        box-shadow: 0 10px 20px rgba(0, 0, 0, 0.33)
    }

    .new-game-btn:active{
        transform: translateY(-1px);
        box-shadow: 0 5px 10px rgba(0, 0, 0, 0.33)
    }

    .chessboard {
        height: 80vh;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }
    .board-header, 
    .board-row {
        display: flex;
    }
    
    .board-header-cell,
    .board-cell {
        width: 60px;
        height: 60px;
        display: flex;
        justify-content: center;
        align-items: center;
    }
  
    .board-cell {
        position: relative;
    }

    .board-cell:hover{
        cursor: pointer;
    }

    .board-cell:before {
        content: '';
        border: 2px solid black;
        position: absolute;
        top: -1px;
        left: -1px;
        right: -1px;
        bottom: -1px;
        background-image: url("https://www.transparenttextures.com/patterns/wood-pattern.png");
        background-color: #B58863;
    }
  
    .board-cell.even:before {
        border: 2px solid black;
        background-color: #F0D9B5;
        background-image: url("https://www.transparenttextures.com/patterns/wood-pattern.png");  
    }
    
    .clicked-cells {
        margin-top: 10px;
    }
    
    .clicked-cells > div {
        margin-right: 5px;
        display: inline-block;
        padding: 5px;
        background-color: #ffffff30;
        border: 1px solid #ccc;
    }

    .selected{
        z-index: 1; 
        box-shadow: 0 0 15px 10px rgb(255, 0, 0);
    }

    @media only screen and (max-width: 600px){
        .board-header-cell,
        .board-cell {
            width: 35px;
            height: 35px;   
    }

    .new-game-btn{
            padding: 5px 10px;
            font-size: 10px;
        }
    
    }

    @media only screen and (max-width: 300px){
        .board-header-cell,
        .board-cell {
            width: 25px;
            height: 25px;
        }
    .new-game-btn{
            padding: 5px 10px;
            font-size: 10px;
        }
    }
  </style>
  