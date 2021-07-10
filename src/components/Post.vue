<template>
  <div class="post-parent">
    <div 
      class="post"
      v-for="item, index in data" 
      :key="item.id"
    >
      <h3>{{ item.title }}</h3>
      <span
        v-if="unClicked"
        @click="unClicked = !unClicked"
      >{{ item.body.substring(0,35)+"...Reveal more" }}</span>
      <span v-else>{{ item.body }}</span>
      <h3>{{ users.find((user) => user.id === item.userId)?.name }}</h3>
      <button
        class="btn" 
        @click="this.data.splice(index, 1)" 
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
      unClicked: true
    }
  },

  methods: {
    async fetchPosts() {
      const url = "https://jsonplaceholder.typicode.com";

    fetch(`${url}/posts`)
      .then(res => { return res.json() })
      .then(json => {
        this.data = json;

        fetch(`${url}/users`)
          .then(res => { return res.json() })
          .then(json => { this.users = json })
      })
      .catch(e => { console.log(e) })
    }
  },
  
  mounted() {
    this.fetchPosts();
  }

};
</script>