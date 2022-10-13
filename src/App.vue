<template>
  <div>
    <div class="post">
      <div><strong>Название:</strong> Пост о JavaScript</div>
      <div><strong>Описание:</strong> Пост о Джеесе</div>
    </div>
    <div class="post">
      <div><strong>Название:</strong> Пост о JavaScript</div>
      <div><strong>Описание:</strong> Пост о Джеесе</div>
    </div>
    <div class="post">
      <div><strong>Название:</strong> Пост о JavaScript</div>
      <div><strong>Описание:</strong> Пост о Джеесе</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      posts: [
        { id: 1, title: 'JavaScript', description: 'Описание JavaScript' },
        { id: 2, title: 'PHP', description: 'Описание PHP' },
        { id: 3, title: 'MySql', description: 'Описание MySql' },
      ]
    }
  },
  methods: {

  },
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .post {
    padding: 15px;
    border: 2px solid teal;
    margin-top: 15px;
  }
</style>