<template>
  <form @submit.prevent>
    <h4> Post creation </h4>
    <my-input
        v-model="post.title"
        type="text"
        placeholder="Post title"
    />
    <my-input
        v-model="post.body"
        type="text"
        placeholder="Post description"
    />
    <my-button
        style = "align-self: flex-end; margin-top: 15px"
        @click="createPost"
    >
      Create
    </my-button>
  </form>
</template>

<script>
import MyInput from "@/components/UI/MyInput";
export default {
  components: {MyInput},
  data() {
    return {
      post: {
        title: '',
        body: ''
      }


    }
  },
  methods: {
    createPost() {
      this.post.id = Date.now()
      this.$emit('create', this.post)
      this.post = {
        title: '',
        body: '',
      }
    },
  },

}
</script>

<style scoped>
form{
  display: flex;
  flex-direction: column;
}
</style>