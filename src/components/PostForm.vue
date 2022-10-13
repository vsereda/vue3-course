<template>
  <form @submit.prevent>
    <h4>Создание поста</h4>
    <input
        v-model="post.title"
        class="input"
        type="text"
        placeholder="Название"
    >
    <input
        v-model="post.description"
        class="input"
        type="text"
        placeholder="Описание"
    >
    <my-button
        style="align-self: flex-end; margin-top: 15px"
        @click="CreatePost"
    >
      Создать
    </my-button>
  </form>
</template>

<script>
import MyButton from "@/components/UI/MyButton";

export default {
  name: "PostForm",
  components: {MyButton},
  data() {
    return {
      post: {
        title: '',
        description: '',
      },
    }
  },
  methods: {
    CreatePost() {
      this.post.id = Date.now()
      this.$emit('create', this.post, '2', '3')
      this.post = {
        title: '',
        description: '',
      }
    },
  },
}
</script>

<style scoped>

form {
  display: flex;
  flex-direction: column;
}

.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}
</style>