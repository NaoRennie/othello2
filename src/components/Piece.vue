<template>
  <div
    class="piece"
    :num="num"
    :style="pieceStyle"
    @click="$emit('clicked')"
    ></div>
</template>

<script> 
export default {
  name: 'Piece',
  props: {
    num: {
      type: Number,
      default: 0
    }
  },
  data (){
    return {
      color:['black', 'white']
    }
  },
  computed: {
    pieceStyle: function(){
      if(this.num===1){
        return {background: this.color[1]}
      } else if (this.num===2){
        return {background: this.color[0]}
      }
      return {background:''}
    },
  }
}
</script>

<style scoped>
.piece {
  display: inline-block;
  border-radius: 50%;
  height: 40px;
  width: 40px;
  margin: 3px;
  z-index: 2;
}

</style>
