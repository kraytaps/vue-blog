<template>
  <div id="show-blogs" v-theme=" 'narrow' ">
    <h1>All Blog Articles</h1>
    <input type="text" v-model="search" placeholder="search blogs">
    <div v-for="blog in filteredBlogs" class="single-blog">
      <router-link v-bind:to="'/blog/' + blog.id"><h2 v-rainbow> {{ blog.title | toUppercase }}</h2></router-link>
      <article>{{ blog.content | snippet }}</article>
    </div>
  </div>
</template>

<script>
import searchMixin from '../mixins/searchMixin';

export default {

  data() {
    return {
      blogs: [],
      search: '',
    }
  },
  methods: {

  },
  created() {
    this.$http.get('https://vue-blog-project-d84dd.firebaseio.com/posts.json').then(function(data){
      return data.json();
    }).then((data) => {
      var blogsArray = [];
      for (let key in data){
        console.log(data[key]);
        data[key].id = key;
        blogsArray.push(data[key]);
      }
      console.log(blogsArray);
      this.blogs = blogsArray;
    });
  },
  computed: {

  },
  filters: {
    // 'to-uppercase': function(value){
    //   return value.toUpperCase();
    // } // one way to instantiate filters
    toUppercase(value){
      return value.toUpperCase();
    },
    snippet(value){
      return value.slice(0, 100) + '...';
    }
  },
  directives: {
    'rainbow': {
      bind(el, binding, vnode){
        el.style.color = '#' + Math.random().toString().slice(2,8)
      }
    },
    'theme': {
      bind(el, binding, vnode){
        if (binding.value == 'wide'){
          el.style.maxWidth = '1200px';
        } else if (binding.value == 'narrow'){
          el.style.maxWidth = '560px';
        }
        if (binding.arg == 'column'){
          el.style.background = '#ddd';
          el.style.padding = '20px';
        }
      }
    }
  },
  mixins: [searchMixin]
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Nunito+Sans&display=swap');
a{
    color: #fff;
    text-decoration: none;
    padding: 6px 8px;
    border-radius: 10px;
}
#show-blogs{
  max-width: 800px;
  margin: 0 auto;
}
.single-blog {
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: #eee;
}
</style>
