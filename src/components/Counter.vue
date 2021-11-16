<template>
  <div>
    <button @click="addLike">Like</button>
    <button @click="addDislike">Dislike</button>
  </div>
  <div>Likes: <strong>{{ likes }}</strong></div>
  <div>Dislike: <strong>{{ dislikes }}</strong></div>
</template>

<script>
  export default {
    data() {
      return {
        likes: 0,
        dislikes: 0,
      }
    },
    methods: {
      addLike() {
        this.likes += 1;
      },
      addDislike() {
        this.dislikes += 1;
      }
    }
  }
</script>

// scoped - этот флаг означает, что стили будут применены только к этому компоненту
<style scoped>

</style>