<template>
  <div>
    <div>
      <button>Like</button>
      <button>Dislike</button>
    </div>
    <div>
      Количество лайков <strong>{{ likes }}</strong>
      Количество дизлайков <strong>{{ dislikes }}</strong>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      likes: 0,
      dislikes: 5,
    }
  }
}
</script>

<style scoped>

</style>