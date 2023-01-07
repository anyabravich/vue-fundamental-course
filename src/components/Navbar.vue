<template lang="">
  <div class="navbar">
    <router-link to="/">Главная</router-link>
    <router-link to="/about">О нас</router-link>
    <button-default @click="$router.push('./posts')">Посты</button-default>
  </div>
</template>
<script>
export default {};
</script>
<style lang="css" scoped>
.navbar {
  display: flex;
  align-items: center;
  background: #212529;
  margin-bottom: 20px;
  padding: 20px 0px;
}

.navbar a {
  color: #fff;
  text-decoration: none;
  padding: 0px 20px;
}
</style>
