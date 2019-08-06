<template>
  <div>
    <app-header></app-header>
    <router-view></router-view>
  </div>
</template>

<script>
import addBlog from './components/addBlog.vue';
import showBlogs from './components/showBlogs.vue';
import listBlogs from './components/listBlogs.vue';
import header from './components/header.vue';

export default {
  components: {
    'add-blog': addBlog,
    'show-blog': showBlogs,
    'list-blog': listBlogs,
    'app-header': header,
  },
  data() {
    return {

    }
  },
  methods: {

  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Nunito+Sans&display=swap');
body {
  margin: 0;
  font-family: 'Nunito Sans', sans-serif;
}
</style>
