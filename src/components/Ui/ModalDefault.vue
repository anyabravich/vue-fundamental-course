<template>
  <div class="modal" v-if="show" @click="hideModal">
    <div class="modal__content" @click.stop>
      <slot></slot>
    </div>
  </div>
</template>
<script>
export default {
  name: "modal-default",
  props: {
    show: {
      type: Boolean,
      default: true,
    },
  },
  methods: {
    hideModal() {
      this.$emit("update:show", false);
    },
  },
};
</script>
<style>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  width: 100%;
  height: 100vh;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal h4 {
  margin-bottom: 15px;
}

.modal__content {
  max-width: 480px;
  width: 100%;
  padding: 20px;
  background: #ffffff;
  border-radius: 10px;
}
</style>
