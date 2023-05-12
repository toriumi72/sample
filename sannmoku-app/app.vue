<script setup lang="ts">
const board = ref(Array(9).fill(null))
const next = ref('X')

const checkWinner = (board:any) => {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ]
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (board[a] && board[a] === board[b] && board[a] === board[c]) {
      return board[a]
    }
  }
  return null
}

const onHandleClick = (i:any) => {
  const newBoard = [...board.value]
  if (checkWinner(newBoard) || newBoard[i]) return
  newBoard[i] = next.value
  board.value = newBoard
  next.value = next.value === 'X' ? 'O' : 'X'
}

const winner = computed(() => checkWinner(board.value))

const onResetGame = () => {
  board.value = Array(9).fill(null)
  next.value = 'X'
}
</script>

<template>
  <div class="text-center">
    <h1 class="">Sannmoku</h1>
  </div>

  <div class="flex flex-wrap w-48 justify-center m-auto mt-10">
    <div v-for="(value, i) in board" :key="i" @click="onHandleClick(i)" class="cell w-16 h-16 border-2 border-black flex justify-center items-center text-2xl">
      {{ value }}
    </div>
    <div v-if="winner" class="w-full text-center mt-10">
      Winner:      
      {{ winner }}
      <button @click="onResetGame" class="mt-5 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
        Play again
      </button>
    </div>
    <div v-else class="w-full text-center mt-10">
      Next player: {{ next }}
    </div>
  </div>
</template>

<style scoped>
</style>




