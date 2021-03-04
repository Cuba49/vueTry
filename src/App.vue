<template>
  <div id="app" class="d-flex justify-content-center">
    <div class="w-75 p-3">
      <h2>Інформація про користувача</h2>
      <hr>
      <AddUser
        @addUser="addUser"
      />
      <hr>
      <p class="text-lg-left">Кількість користувачів: <b>{{users.length}}</b></p>
      <UserList
        :users="users"
      />
    </div>
  </div>
</template>

<script>
import AddUser from "@/components/AddUser";
import UserList from "@/components/UserList";
export default {
  name: 'App',
  components: {
    AddUser,
    UserList
  },
  methods:{
    addUser(user){
      let id = Math.max.apply(Math, this.users.map(function(o) { return Number(o.Id); }))+1;
      this.users.push({Id:id, Name:user.Name, Mail:user.Mail, Age:user.Age});
    }
  },
  data() {
    return {
      users: [{Id:"1", Name:"петро", Mail:"dsfjds", Age:"25"}]
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
