<template>
  <div>
    <Error v-for="error of errors.All" :error="error"/>
    <Error v-for="error of errors.Name" :error="error"/>
    <Error v-for="error of errors.Mail" :error="error"/>
    <Error v-for="error of errors.Age" :error="error"/>
    <form @submit.prevent="$emit('addUser',newUser);clearFields()">
      <div class="row g-3">
        <div class="col-sm-5">
          <input v-model="newUser.Name" @keyup="nameChange()" @change="nameChange()" type="text" class="form-control" placeholder="Your Name">
        </div>
        <div class="col-sm-5">
          <input v-model="newUser.Mail" @keyup="mailChange()" @change="mailChange()" type="email" class="form-control" placeholder="Your Email">
        </div>
        <div class="col-sm">
          <input v-model="newUser.Age" @keyup="ageChange()" @change="ageChange()" type="text" class="form-control" placeholder="Your Age">
        </div>
      </div>
      <br>
      <div class="col">
        <button @click="empty()" :disabled="this.errors.Name.length>0||this.errors.Mail.length>0||this.errors.Age.length>0||this.errors.All.length>0" type="submit" class="btn btn-primary">Add User</button>
      </div>
    </form>
  </div>

</template>

<script>
import Error from "@/components/Error";
export default {
  name: "AddUser",
  components: {Error},
  methods:{
    clearFields(){
          this.newUser={Name:"", Mail:"", Age:""}
    },
    empty(){
        this.errors.All=[];
        if(this.newUser.Name.length==0&&this.newUser.Mail.length==0&&this.newUser.Age.length==0){
            this.errors.All.push("Форма не може бути порожньою!")
            return false;
        }
    },
    nameChange(){
      this.empty();
      this.errors.Name=[];
      if(this.newUser.Name.length>20){
        this.errors.Name.push("Your Name: Довжина має не перевищувати 20 символів")
      }
    },
    mailChange(){
      this.empty();
      this.errors.Mail=[];
      if(!this.regEmail.test(this.newUser.Mail)){
        this.errors.Mail.push("Your Email: Неправильно введена пошта")
      }
    },
    ageChange(){
      this.empty();
      this.errors.Age=[];
      if(this.newUser.Age.length>0&&!this.regAge.test(this.newUser.Age)){
        this.errors.Age.push("Your Age: Мають бути введені лише цифри");
      }
      if(this.newUser.Age.length>3){
        this.errors.Age.push("Your Age: Довжина має бути не більше 3х");
      }
    }
  },
  data(){
    return{
      errors:{All:[],Name:[],Mail:[],Age:[]},
      newUser:{Name:"", Mail:"", Age:""},
      regEmail: /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,24}))$/,
      regAge:/^[0-9]+$/
    }
  }
}
</script>

<style scoped>

</style>