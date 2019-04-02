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
   data () {
     return {
       board:[[0,0,0,0,0,0,0,0],
             [0,0,0,0,0,0,0,0],
             [0,0,0,0,0,0,0,0],
             [0,0,0,1,2,0,0,0],
             [0,0,0,2,1,0,0,0],
             [0,0,0,0,0,0,0,0],
             [0,0,0,0,0,0,0,0],
             [0,0,0,0,0,0,0,0]],
       directions:[[0,-1],[1,0],[0,1],[-1,0],[-1,-1],[1,1],[-1,1],[1,-1]],
       turn: 1
     }
   },
   watch: {
     board: function (){
       this.turn = this.turn *= -1
     }
   },
   methods: {
     clickPiece(x, y) {
       // eslint-disable-next-line 
       console.log(this.turn, 'turn')
       let myColor = '';
       let oponentColor = '';
       this.board = [...this.board]
       this.board[y - 1] = [...this.board[y - 1]]
       if(this.turn === 1) {
         myColor = 1
         oponentColor = 2
         let confirmedPieces = []
         this.directions.forEach((i) => {
           let a = y - 1
           let b = x - 1
           let c = i[0]
           let d = i[1]
           let xx = b + c < 0 || b + c > 7 ? b : b + c
           let yy = a + d < 0 || a + d > 7 ? a : a + d
           let candidates = [];
           let n = 1; 
           if(this.board[yy][xx] === oponentColor) {
             candidates.push({ x:xx, y:yy },{ x:b, y:a })
             while(candidates.length > 0){
               if(this.board[yy + d * n][xx + c * n] === 0) {
                 break;
               }else if (this.board[yy + d * n][xx + c * n] === oponentColor) {
                 candidates.push({ x:xx + c * n, y:yy + d * n });
                 // eslint-disable-next-line 
                 console.log('hothohtohtohto')
                 n += 1;
               } else {
                 confirmedPieces.push(...candidates)
                 break;
               }
             }
            confirmedPieces.forEach((i) =>{
            return this.board[i.y][i.x] = myColor
             })
             confirmedPieces.length=0
           }   
         })
       } else if (this.turn === -1) {
        myColor = 2
         oponentColor = 1
         let confirmedPieces = []
         this.directions.forEach((i) => {
           let a = y - 1
           let b = x - 1
           let c = i[0]
           let d = i[1]
           let xx = b + c < 0 || b + c > 7 ? b : b + c
           let yy = a + d < 0 || a + d > 7 ? a : a + d
           let candidates = [];
           let n = 1; 
           if(this.board[yy][xx] === oponentColor) {
             candidates.push({ x:xx, y:yy },{ x:b, y:a })
             while(candidates.length > 0){
               if(this.board[yy + d * n][xx + c * n] === 0) {
                 break;
               }else if (this.board[yy + d * n][xx + c * n] === oponentColor) {
                 candidates.push({ x:xx + c * n, y:yy + d * n });
                 n += 1;
               } else {
                 confirmedPieces.push(...candidates)
                 break;
               }
             }
            confirmedPieces.forEach((i) =>{
            return this.board[i.y][i.x] = myColor
             })
             confirmedPieces.length=0
           }   
         }) 
       }
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
