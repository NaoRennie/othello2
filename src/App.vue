<template>
  <div class = "board">
    <div class = "row" v-for="y in 8" :key="y">
      <div
        class= "square"
        v-for="x in 8"
        :key="x"
        >
        <Piece
        :num="board[y - 1][x - 1]"
        @clicked="clickPiece(x, y)"
         ></Piece>
      </div>
    </div>
  </div>
</template>

<script>
import Piece from './components/Piece'
export default {
    name: 'App',
    components: {
    Piece
  },
   props: {
    num: {
      type: Number,
      default: 0
    }
   },
  data (){
    return {
      board:[[3,3,3,3,3,3,3,3],
             [3,0,0,0,0,0,0,3],
             [3,0,0,0,0,0,0,3],
             [3,0,0,1,2,0,0,3],
             [3,0,0,2,1,0,0,3],
             [3,0,0,0,0,0,0,3],
             [3,0,0,0,0,0,0,3],
             [3,3,3,3,3,3,3,3]],
      directions:[[0,-1],[1,0],[0,1],[-1,0],[-1,-1],[1,1],[-1,1],[1,-1]]
    }
  },
  // watch: {
  //   board: 
  // },
  // mounted() {
  //   this.piece = JSON.parse(localStorage.getItem('pieces')) || [];
  // },
  // watch: {
  //   piece: function(){
  //     localStorage.setItem('pieces', JSON.stringify(this.piece))
  //   }
  // },
   methods: {
    clickPiece(x, y){
      // eslint-disable-next-line
      console.log(this.board, x, 'HHH')
      let changeColor=[];
      this.board = [...this.board]
      this.board[y - 1] = [...this.board[y - 1]]
      this.directions.forEach((i) => {
        let xx = x - 1 + i[0]
        let yy = y - 1 + i[1]
        let a = y - 1
        let b = x - 1
         // eslint-disable-next-line
      console.log(yy, xx, 'HHH')
        if(this.board[xx][yy]===1){
          return changeColor.push({x:b, y:a})
        }
        return this.board[a][b] = 0
      })
      // eslint-disable-next-line
      console.log(this.board)
     changeColor.forEach((i) =>{
       return this.board[i.y][i.x]=1
     })
      
    }
  }
}
</script>

<style scoped>
.board {
  background-color: green;
  height: 400px;
  width: 400px;
}

.square {
  display: inline-block;
  border: 1px  solid black;
  height: 50px;
  width: 50px;
  z-Index: 1;
}
.row {
  border: 1px black;
  height: 50px;
  /* width: 100px; */
  display: flex;
}
</style>
