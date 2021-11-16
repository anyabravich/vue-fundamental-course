<template lang="">
  <button class="btn" type="button">
    <slot></slot>
  </button>
</template>
<script>
export default {
  name: 'button-default'
}
</script>
<style scoped>
  .btn {
    padding: 10px 15px;
    color: teal;
    border: 3px solid teal;
    /* border-radius: 5px; */
    background: transparent;
    font-weight: 700;
    transition: color 100ms linear;
    cursor: pointer;
    outline: none;
  }

  .btn:hover {
    background: teal;
    color: white;
    transition: color 100ms linear;
  }
</style>