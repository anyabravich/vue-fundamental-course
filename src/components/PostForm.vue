<template lang="">
  <form class="form">
    <h4>Создание поста</h4>
    <input-default 
      v-model="post.title"
      type="text" 
      name="title" 
      placeholder="Название"
    />
    <input-default 
      v-model="post.body" 
      type="text" 
      name="body" 
      placeholder="Описание"
    />
    <button-default 
      type="button"
      @click="createPost"
    >
      Создать
    </button-default>
  </form>
</template>
<script>

export default {
  data() {
    return {
      post: {
        title: '',
        body: ''
      }
    }
  },
  methods: {
    createPost() {
      this.post.id = Date.now();
      this.$emit('create', this.post)
      this.post = {
        title: '',
        body: ''
      }
    }
  },
}
</script>
<style scoped>
  .form {
    padding: 15px 0px;
  }

  h4 {
    margin-bottom: 10px;
  }
</style>