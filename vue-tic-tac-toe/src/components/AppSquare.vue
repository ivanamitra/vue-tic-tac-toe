<template>
    <div id="app-square" @click="squareClicked">
        {{ !!square ? square : '' }}
    </div>
</template>

<script>
export default {
  name: 'AppSquare',
  props: {
    square: String
  },
  methods: {
    squareClicked() {
      if (!this.square) this.$emit('squareClicked');
    }
  }
}
</script>

<style scoped>