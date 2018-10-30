<template>
  <p>{{txt}}</p>
</template>

<script>
export default {
  props: {
    txt: {
      type: String,
      default: ''
    }
  }
}
</script>

<style scoped>
p{
 font-size: 0.8em;
 color: #333;
 margin: 1em 1em;
}
</style>

