<template lang="">
  <div>
    <button-default 
      v-for="page in totalPages" 
      :key="page"
      :class="{
        'pagination-btn': true,
        'pagination-btn-current': page === currentPage
      }"
      @click="getNumberPage(page)"
    >
      {{ page }}
    </button-default>
  </div>
</template>
<script>
export default {
  name: 'pagination-default',
  props: {
    totalPages: {
      type: Number
    },
    currentPage: {
      type: Number
    },
    modelValue: {
      type: Number
    }
  },
  methods: {
    getNumberPage(pageNumber) {
      this.$emit('update', pageNumber);
    }
  }
}
</script>
<style lang="css" scoped>
  .pagination-btn {
    margin-right: 15px;
  }

  .pagination-btn:last-child {
    margin-right: 0;
  }
  .pagination-btn-current {
    color: #fff;
    background: teal;
  }
</style>