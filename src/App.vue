<script setup>
  import { ref, computed } from 'vue'

  const player = ref('X');
  const board = ref([
    ['','',''],
    ['','',''],
    ['','',''],
])

const calculateWinner = (square) => {
  const lines = [
    [0,1,2],
    [3,4,5],
    [6,7,8],
    [0,3,6],
    [1,4,7],
    [2,5,8],
    [0,4,8],
    [2,4,6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a,b,c] = lines[i];
    if (square[a] && square[a] === square[b] && square[a] === square[c]) {
      return square[a];
    }
  }
  return null;
}

const winner = computed(() => calculateWinner(board.value.flst()))

const makeMove = ( x, y) => {
  if (winner.value) return

  if (board.value[x][x] !== '') return

  board.value[x][y] = player.value
  player.value = player.value === 'X' ? 'O' : 'X'
}

const resetGame = () => {
  board.value = [
    ['','',''],
    ['','',''],
    ['','',''],
  ]
  player.value = 'X' 
}

</script>

<template>
  <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1>
</template>

<style>

</style>
