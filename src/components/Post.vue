<template>
  <div class="post-parent">
    <div 
      class="post"
      v-for="item, index in data" 
      :key="item.id"
    >
      <h3>{{ item.title }}</h3>
      <span> {{ item.body }} </span>
      <h3>{{ users.find((user) => user.id === item.userId)?.name }}</h3>
      <button
        class="btn" 
        @click="deletePost(index)" 
      >
        Delete
      </button>
    </div>
  </div>
</template>

<script>

export default {
  name: "Post",


  data() {
    return {
      data: [],
      users: [],
    }
  },

  methods: {
    deletePost(index) {
      this.data.splice(index, 1)
    }
  },

  mounted() {
    const url = "https://jsonplaceholder.typicode.com";

    fetch(`${url}/posts`)
      .then((res) => { return res.json() })
      .then((json) => {
        this.data = json;

        fetch(`${url}/users`)
          .then((res) => { return res.json() })
          .then((json) => { this.users = json })
      })
      .catch(e => { console.log(e) })
  }
};
</script>