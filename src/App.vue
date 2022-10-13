<template>
  <div class="app">
    <post-form
        @create="createPost"
    >
    </post-form>
    <post-list
        :posts="posts"
    >

    </post-list>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";

export default {
  name: "App",
  components: {
    PostList, PostForm,
  },
  data() {
    return {
      posts: [
        {id: 1, title: 'JavaScript', description: 'Описание JavaScript'},
        {id: 2, title: 'PHP', description: 'Описание PHP'},
        {id: 3, title: 'MySql', description: 'Описание MySql'},
        {id: 4, title: 'Python', description: 'Описание Python'},
      ],
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post)
    },
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}

</style>