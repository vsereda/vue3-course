<template>
  <div>
    <h1>Страница с постами</h1>
    <my-input v-model="searchQuery" v-focus placeholder="Поиск... "/>
    <div class="app__btns">
      <my-button @click="showDialog">
        Создать посьт
      </my-button>
      <my-select
          v-model="selectedSort"
          :options="sortOptions"
      />
    </div>
    <my-dialog v-model:show="dialogVisible">
      <post-form
          @create="createPost"
      >
      </post-form>
    </my-dialog>
    <post-list
        :posts="sortedAndSearchedPosts"
        @remove="removePost"
        v-if="!isPostsLoading"
    >
    </post-list>
    <div v-else>Идет загрузка...</div>
    <div
        v-intersection="loadMorePosts"
        class="observer"
    >

    </div>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import axios from 'axios';
import MyButton from "@/components/UI/MyButton";
import MySelect from "@/components/UI/MySelect";
import MyInput from "@/components/UI/MyInput";

export default {
  name: "post-page",
  components: {
    MyInput,
    MySelect,
    MyButton,
    PostList, PostForm,
  },
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostsLoading: false,
      limit: 10,
      page: 1,
      searchQuery: '',
      selectedSort: '',
      sortOptions: [
        {value: 'title', name: 'Поназванию'},
        {value: 'body', name: 'По содержанию'},
      ],
      totlalPages: 0,
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    showDialog() {
      this.dialogVisible = true;
    },
    // changePage(pageNumber) {
    //   this.page = pageNumber
    // },
    async fetchPosts() {
      try {
        this.isPostsLoading = true;
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
          params: {
            _page: this.page,
            _limit: this.limit,
          }
        });
        this.totlalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
        this.posts = response.data;
      } catch (e) {
        alert('Ошибочка')
      } finally {
        this.isPostsLoading = false;
      }
    },
    async loadMorePosts() {
      try {
        this.page += 1;
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
          params: {
            _page: this.page,
            _limit: this.limit,
          }
        });
        this.totlalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
        this.posts = [...this.posts, ...response.data];
      } catch (e) {
        alert('Ошибочка')
      }
    },
  },
  mounted() {
    this.fetchPosts();

    // const options = {
    //   rootMargin: '0px',
    //   threshold: 1.0
    // }
    //
    // const callback = (entries, observe) => {
    //   if (entries[0].isIntersecting && this.page < this.totlalPages) {
    //     this.loadMorePosts()
    //   }
    // }
    //
    // const observer = new IntersectionObserver(callback, options);
    // observer.observe(this.$refs.observer);
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
    },
    sortedAndSearchedPosts() {
      return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
    },
  },
  watch: {
    // page() {
    //   this.fetchPosts()
    // }
  },
}
</script>

<style>

.app__btns {
  display: flex;
  justify-content: space-between;
  margin: 15px 0;
}

.page__wrapper {
  display: flex;
  margin-top: 15px;
}

.page {
  border: 1px solid black;
  padding: 10px;
}

.current-page {
  border: 2px solid teal;
}

.observer {
  height: 30px;
  background: green;
}

</style>