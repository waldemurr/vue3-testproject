<template>
  <div class="app">
    <h1> Posts page </h1>
<!--    <input type="text" v-model.trim="modifierValue">-->
    <my-button
        @click="showDialog"
        style="margin: 15px 0"
    > Create post </my-button>
    <my-dialog v-model:show="dialogVisible">
      <post-form
          @create="createPost"
      />
    </my-dialog>

    <post-list
        :posts="posts"
        @remove="removePost"
        v-if="!isPostsLoading"
    />
    <div>Fetching posts...</div>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import MyDialog from "@/components/UI/MyDilaog";
import MyButton from "@/components/UI/MyButton";
import axios from "axios";
export default {
  components: {MyButton, MyDialog, PostList, PostForm},
  data() {
    return {
      posts: [
      ],
      dialogVisible: false,
      modifierValue: "",
      isPostsLoading: false,
    }

  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.dialogVisible = false
    },
    removePost(post){
      this.posts  = this.posts.filter(p => p.id !== post.id)
    },
    showDialog(){
      this.dialogVisible = true
    },
    async fetchPosts(){
      try{
        setTimeout( async () => {
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
          this.posts = response.data;
        }, 1000);

      } catch (e){
        alert('Error occured');
      }
    },
  },
  mounted: function () {
    this.fetchPosts();
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
box-sizing: border-box;
}
.app{
  padding: 20px;
}
</style>