<template>
  <form @submit.prevent>
    <h4>Создание поста</h4>
    <input
        v-bind:value="title"
        @input="title = $event.target.value"
        class="input"
        type="text"
        placeholder="Название"
    >
    <input
        v-bind:value="description"
        @input="description = $event.target.value"
        class="input"
        type="text"
        placeholder="Описание"
    >
    <button
        class="btn"
    >
      Создать
    </button>
  </form>
</template>

<script>
export default {
  name: "PostForm",
  data() {
    return {
      // posts: [
      //   {id: 1, title: 'JavaScript', description: 'Описание JavaScript'},
      //   {id: 2, title: 'PHP', description: 'Описание PHP'},
      //   {id: 3, title: 'MySql', description: 'Описание MySql'},
      //   {id: 4, title: 'Python', description: 'Описание Python'},
      // ],
      // title: '',
      // description: '',
    }
  },
}
</script>

<style scoped>

form {
  display: flex;
  flex-direction: column;
}

.btn {
  margin-top: 15px;
  align-self: flex-end;
  padding: 10px 15px;
  background: none;
  color: teal;
  border: 1px solid teal;
}

.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}
</style>