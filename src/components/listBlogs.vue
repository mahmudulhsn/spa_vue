<template>
  <div v-theme:column="'narrow'" id="show-blogs">
    <h1>All Blogs</h1>
    <input type="search" v-model="search" placeholder="Search Blog">
    <div v-for="blog in filterBlogs0" class="single-blog">
      <h3 v-rainbow>{{ blog.title | to-uppercase }}</h3>
    </div>

  </div>
</template>

<script>
import searchMixin from '../mixins/searchMixin';
export default {
  data () {
    return {
      blogs: [],
      search: '',
    }
  },
  created() {
    this.$http.get('https://jsonplaceholder.typicode.com/posts').then(function(data){
      this.blogs = data.body.slice(0, 10);
    })
  },
  computed: {

  },
  mixins:[searchMixin]
}
</script>

<style>
#show-blogs{
    max-width: 800px;
    margin: 0px auto;
}
.single-blog{
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
}
</style>
