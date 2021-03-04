<template>
  <table class="table">
    <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Name</th>
      <th scope="col">Email</th>
      <th scope="col">Age</th>
    </tr>
    </thead>
    <tbody>
        <User v-for="user of users" :user="user"/>
    </tbody>
  </table>
</template>

<script>
import User from "@/components/User"
export default {
  name: "UserList", 
  components:{
    User
  },
  props:["users"]
}
</script>

<style scoped>

</style>