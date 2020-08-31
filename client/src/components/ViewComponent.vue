<template>
  <div class="container">
    <h1>Latest Orders</h1>
    
    <hr>
    <p class="error" v-if="error">{{ error }}</p>
    <div class="posts-container">
      <div class="post" 
      v-for="(post, index) in posts"
      v-bind:item="post"
      v-bind:index="index"
      v-bind:key="post._id"
      >
        {{ `${post.createdAt.getDate()}/${post.createdAt.getMonth()}/${post.createdAt.getFullYear()}` }}
        <p class="text">{{ post.text }}</p>
        <button class="cartButton" type="button" v-on:click="removeItem(post)">Order Completed</button>
        <br><br>
      </div>
    </div>
  </div>
</template>

<script>
import PostService from '../PostService.js';

export default {
  name: 'PostComponent',
  data() {
    return {
      posts:[],
      error: '',
      text: ''
    }
  },
  async created(){
    try{
      this.posts = await PostService.getPosts();
    } catch(err){
      this.error = err.message;
    }
  },
  methods:{
    async removeItem(post){
      if(confirm("are you sure you want to delete '"+post.text+"'?")){
        await PostService.deletePost(post._id);
        this.posts = await PostService.getPosts();
      }
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
