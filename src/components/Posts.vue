<template>
  <div id="posts-header"> 
    <h1>Posts</h1>

    <div id="posts-content">
      <div
        class="post-parent"
        v-for="item in data"
        :key="item.id"
      >
        <div class="post">
          <h3> {{ item.title }} </h3>
          <span> {{ item.body }} </span>
          <h3> {{ users.find(person => person.id === item.userId)?.name }} </h3>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
    name: "Posts",
    data() {
      return {
        data: [],
        users: []
      }
    },
    mounted() {

      const url = 'https://jsonplaceholder.typicode.com'

      fetch(`${url}/posts`)
        .then(res => { return res.json() })
        .then(json => {
          this.data = json
          console.log(this.data)

          fetch(`${url}/users`)
            .then((res) => {
              return res.json()
            })
            .then(json => {
              this.users = json
              console.log(this.users)
            })
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