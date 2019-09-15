<template>

  <div id="single-blog">
    <h1>{{ blog.title }}</h1>
    <article>{{ blog.content }}</article>
    <p><strong>Author: </strong>{{ blog.author }}</p>
    <p> <strong>Category:</strong> </p>
    <ul>
      <li v-for="category in blog.categories">{{ category }}</li>
    </ul>
  </div>

</template>


<script>
export default {
  data() {
    return {
      id:this.$route.params.id,
      blog:{}
    }
  },
  created() {
    this.$http.get('https://fir-487cf.firebaseio.com/posts/'+this.id+'.json').then(function(data){
      return data.json();
    }).then(function(data){
      this.blog = data;
    });
  },
}
</script>
<style lang="">
  #single-blog{
      max-width: 960px;
      margin: 0 auto;
  }
</style>

