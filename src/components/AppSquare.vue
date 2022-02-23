<template>
    <div id="app-square" @click="$emit('squareClicked')">
        {{  square }}
    </div>
</template>

<script>
export default {
  name: 'AppSquare',
  props: {
    square: String
  }
}
</script>

<style scoped>