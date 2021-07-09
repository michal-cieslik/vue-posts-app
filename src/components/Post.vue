<template>
  <div class="post-parent">
    <div
      class="post-query-section"
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
</template>

<script>

export default {
    name: "Post",
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