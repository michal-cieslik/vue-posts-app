<template>
  <div id="posts-header"> 
    <h1>Posts</h1>

    <div id="posts-content">
      <Post />
    </div>
  </div>
</template>

<script>
import Post from './Post.vue'

export default {
    name: 'Wrapper',
    components: {
        Post
    }
}
</script>