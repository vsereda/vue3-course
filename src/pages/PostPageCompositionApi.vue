<template>
  <div>
    <h1>Страница с постами</h1>
    <my-input v-model="searchQuery" v-focus placeholder="Поиск... "/>
    <div class="app__btns">
      <my-button
      >
        Создать посьт
      </my-button>
      <my-select
          v-model="selectedSort"
          :options="sortOptions"
      />
    </div>
    <my-dialog v-model:show="dialogVisible">
      <post-form
      >
      </post-form>
    </my-dialog>
    <post-list
        :posts="sortedAndSearchedPosts"
        v-if="!isPostsLoading"
    >
    </post-list>
    <div v-else>Идет загрузка...</div>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import axios from 'axios';
import MyButton from "@/components/UI/MyButton";
import MySelect from "@/components/UI/MySelect";
import MyInput from "@/components/UI/MyInput";
import {ref} from "vue";
import useSortedPosts from "@/hooks/useSortedPosts";
import {usePosts} from "@/hooks/usePosts";
import useSortedAndSearchedPosts from "@/hooks/useSortedAndSearchedPosts";

export default {
  name: "post-page-composition-api",
  components: {
    MyInput,
    MySelect,
    MyButton,
    PostList, PostForm,
  },
  data() {
    return {
      dialogVisible: false,
      sortOptions: [
        {value: 'title', name: 'Поназванию'},
        {value: 'body', name: 'По содержанию'},
      ],
    }
  },
  setup(props) {
    const {isPostsLoading, posts, totalPages} = usePosts(10);
    const {sortedPosts, selectedSort} = useSortedPosts(posts);
    const {searchQuery, sortedAndSearchedPosts} = useSortedAndSearchedPosts(sortedPosts);

    return {
      posts,
      totalPages,
      isPostsLoading,
      selectedSort,
      searchQuery,
      sortedAndSearchedPosts,
    }
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