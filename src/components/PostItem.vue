<template>
  <div class="post">
    <div>
      <div><strong>Номер: </strong>{{ post.id }}</div>
      <div><strong>Название: </strong>{{ post.title }}</div>
      <div><strong>Описание: </strong>{{ post.body }}</div>
    </div>
    <div class="post__buttons">
      <button-default @click="$router.push(`/posts/${post.id}`)">
        Открыть
      </button-default>
      <button-default @click="$emit('remove', post)"> Удалить </button-default>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
};
</script>
<style scoped>
.post {
  display: flex;
  align-items: center;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 15px;
  padding: 15px;
  border: 3px solid teal;
}

.post:last-child {
  margin-bottom: 0px;
}

.post__buttons {
  display: flex;
  margin-left: 20px;
}

.post__buttons .btn:first-child {
  margin-right: -3px;
}
</style>
