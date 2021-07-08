<template>
  <div id="posts-header"> 
    <h1>Posts</h1>

    <div id="posts-content">
      <div
        v-for="item of data" 
        :key="item.id"
        class="post-parent"
      >
        <div class="post">
          <h4> {{ item.title }} </h4>
          <span> {{ item.body }} </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
    name: "Posts",
    data() {
      return {
        data: []
      }
    },
    created() {
      const url = 'https://jsonplaceholder.typicode.com'

        axios
          .get(`${url}/posts`)
          .then((res) => {
            console.log(res)
          })
          .catch(error => {
            console.log(error)
          })
      }
    }
</script>

<style>
.post-parent {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.post{
  font-family: 'Helvetica';
  text-align: center;
  color: #2c3e50;
  padding: 25px;
  margin-bottom: 25px;
  height: 200px;
  width: 75vh;
  border-radius: 8px;
  box-shadow: 0 4px 12px 0 rgba(0, 0, 0, 0.08);
  background-color: #f9f9f9;
}
</style>