<template>
  <div id="add-blog">

    <h2> Add New Blog Post</h2>
    <form v-if="!submitted">
      <label for="">Blog Title: </label>
      <input type="text" v-model.lazy="blog.title" required>

      <label for="">Blog Content</label>
      <textarea v-model.lazy="blog.content"></textarea>

      <div id="checkboxes">
        <label for="">Sports</label>
        <input type="checkbox" value="sports" v-model="blog.categories">
        <label for="">National</label>
        <input type="checkbox" value="national" v-model="blog.categories">
        <label for="">Entertainemnt</label>
        <input type="checkbox" value="entertainemnt" v-model="blog.categories">
        <label for="">Others</label>
        <input type="checkbox" value="others" v-model="blog.categories">
      </div>

      <label for="">Author: </label>
      <select v-model="blog.author">
        <option v-for="author in authors">{{ author }}</option>
      </select>
      <button v-on:click.prevent="post">Add Post</button>
    </form>

    <div v-if="submitted">
      <h3> Posts Added Successfully. </h3>
    </div>

    <div id="preview">
      <h3>Preview</h3>
      <p>Blog Title:{{ blog.title }}</p>
      <p>Blog Content:</p>
      <p>{{ blog.content }}</p>
      <p>Categories: </p>
      <ul>
        <li v-for="category in blog.categories">{{ category }}</li>
      </ul>
      <p>Authors: {{ blog.author }}</p>
    </div>


  </div>
</template>

<script>
export default {
  components:{

  },
  data () {
    return {
      blog:{
        title: '',
        content: '',
        categories: [],
        author: '',
      },
      authors:['Mahmudul', 'Hasan', 'Hasib'],
      submitted: false,

    }

  },
  methods: {
      post: function(){
        this.$http.post('https://fir-487cf.firebaseio.com/posts.json', this.blog).then(function(data){
          console.log(data);
          this.submitted = true;
        });
      },
    },
}
</script>

<style>
#add-blog *{
    box-sizing: border-box;
}
#add-blog{
    margin: 20px auto;
    max-width: 500px;
}
label{
    display: block;
    margin: 20px 0 10px;
}
input[type="text"], textarea{
    display: block;
    width: 100%;
    padding: 8px;
}
#preview{
    padding: 10px 20px;
    border: 1px dotted #ccc;
    margin: 30px 0;
}
h3{
    margin-top: 10px;
}
#checkboxes label{
    display: inline-block;
}
#checkboxes input{
  display: inline-block;
  margin-right: 10px;
}
</style>
