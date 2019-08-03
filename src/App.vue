<template>
  <div>
  <add-blog></add-blog>
  </div>
</template>

<script>

export default {
  import addBlog from './components/addBlog.vue';

  components: {
    'add-blog': addBlog;
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
body {
  margin: 0;
  font-family: 'Nunito SemiBold', sans-serif;
}
</style>
