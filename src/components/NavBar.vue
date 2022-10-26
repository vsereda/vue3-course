<template>
  <div class="navbar">
    <div @click="$router.push('/')">
      Vue 3
    </div>
    <div class="nav__btns">
      <my-button @click="$router.push('/posts')">Посты</my-button>
      <my-button @click="$router.push('/about')" style="margin-left: 20px">О сайте</my-button>
      <my-button @click="$router.push('/store')" style="margin-left: 20px">store</my-button>
    </div>
  </div>
</template>

<script>
export default {
  name: "nav-bar",
  components: {}

}
</script>

<style scoped>

.navbar {
  height: 50px;
  background-color: lightgray;
  box-shadow: 2px 2px 4px gray;
  display: flex;
  align-items: center;
  padding: 0 15px;
}

.nav__btns {
  margin-left: auto;
}

</style>