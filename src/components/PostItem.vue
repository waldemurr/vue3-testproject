<template>
  <div class="post">
    <div>
      <div><strong> Topic: </strong> {{post.title}}</div>
      <div><strong> Preview: </strong> {{post.body}}</div>
    </div>
    <div class="post__buttons">
      <my-button
          @click="$emit('remove', post)"
      >
        Remove
      </my-button>
    </div>
  </div>
</template>

<script>
export default {
  name: "PostItem",
  props: {
    post: {
      type: Object,
      required: true,
    }
  }
}
</script>

<style scoped>
  .post {
    padding: 15px;
    border: 10px solid darkslateblue;
    margin-top: 15px;
    border-radius: 5px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
</style>