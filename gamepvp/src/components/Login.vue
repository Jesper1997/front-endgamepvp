<template>
    <form @submit="CheckSubmit">
        <div>
            <div class="alert alert-warning" v-bind:key="index" v-for="(error, index) in errors">{{error}}</div>
            <h4>username</h4>
            <input type="text" v-model="name" name="name" placeholder="insery username">
            <h4>password</h4>
            <input type="password" v-model="password" name="password" placeholder="Insert password">
            <br>
            <input v-on:click="loginUser" type="Submit" value="Login" class="btn">
            <input v-on:click="createAccount" value="Create Account" type="Submit" class="btn">
        </div>
    </form>
</template>

<script>
export default {
    name: "Login",
    data(){
        return{
            name: "",
            password: "",
            submit : false,
            errors :[]
        }
    },
    methods:{
        CheckSubmit(e){
            e.preventDefault();
            this.errors = [];
            if(!this.name){
                this.errors.push("name is requiered")
            }
            if(!this.password){
                this.errors.push("Password is requierd")
            }
            if(this.submit)
            {
                if(this.errors.length === 0){
                    console.log("hello")
                    const login = {
                        Name: this.name,
                        Pw: this.password
                    }
                    this.$emit('Login',login);
                    this.submit = false;
                }
            }

        },
        loginUser(){
           this.submit = true;
        },
        createAccount(){
            this.$emit('createaccount');
        }

    }
}
</script>

<style scoped>
body{
    background-color: #ffffff;
}
  input[type="text"] {
    flex: 10;
    padding: 5px;
  }
  input[type="submit"] {
    flex: 2;
  }

  .btn{
      padding-left: 10px;
      padding-right: 10px;
      margin-top: 10px;
      cursor: pointer;
      color: black;
  }
  .btn:hover{
      color:gray;
    }
</style>