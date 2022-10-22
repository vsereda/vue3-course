<template>
  <form @submit.prevent>
    <h4>Создание поста</h4>
    <my-input
        v-model="post.title"
        type="text"
        placeholder="Название"
    ></my-input>
    <my-input
        v-model="post.body"
        type="text"
        placeholder="Описание"
    ></my-input>
    <my-button
        style="align-self: flex-end; margin-top: 15px"
        @click="CreatePost"
    >
      Создать
    </my-button>
  </form>
</template>

<script>

import MyInput from "@/components/UI/MyInput";
export default {
  name: "PostForm",
  components: {MyInput},
  data() {
    return {
      post: {
        title: '',
        body: '',
      },
    }
  },
  methods: {
    CreatePost() {
      this.post.id = Date.now()
      this.$emit('create', this.post, '2', '3')
      this.post = {
        title: '',
        body: '',
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

</style>