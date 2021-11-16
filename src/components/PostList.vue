<template lang="">
  <div class="post-list post-list-move" v-if="posts.length > 0">
    <h4>Список постов</h4>
    <transition-group name="post-list">
      <post-item 
        v-for="post in posts" 
        :post="post"
        :key="post.id"
        @remove="$emit('remove', post)"
      />
    </transition-group>
  </div>
  <h4 v-else>
    Список постов пуст
  </h4>
</template>
<script>
import PostItem from '@/components/PostItem.vue';

export default {
  components: {
    PostItem
  },
  props: {
    posts: {
      type: Array,
      required: true
    }
  }  
}
</script>
<style scoped>
  .post-list h4 {
    margin-bottom: 10px;
  }

  .post-list-item {
    display: inline-block;
    margin-right: 10px;
  }

  .post-list-enter-active,
  .post-list-leave-active {
    transition: all 0.4s ease;
  }

  .post-list-enter-from,
  .post-list-leave-to {
    opacity: 0;
    transform: translateX(130px);
  }
  .post-list-move {
    transition: transform 0.4s ease;
  }

</style>