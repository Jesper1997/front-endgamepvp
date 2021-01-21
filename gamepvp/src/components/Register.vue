<template>
    <form @submit="CheckSubmit">
        <div>
            <div class="alert alert-warning" v-bind:key="index" v-for="(error, index) in errors">{{error}}</div>
            <h4>insert username</h4>
            <input type="text" v-model="name" name="name" placeholder="insery username">
            <h4> insert password</h4>
            <input type="password" v-model="password" name="password" placeholder="Insert password">
            <h4>insert the same password</h4>
            <input type="password" v-model="passwordcheck" name="passwordcheck" placeholder="Insert the same password">
            <br>
            <input v-on:click="createAccount" value="Create Account" type="Submit" class="btn">
        </div>
    </form>
</template>

<script>
export default {
    name: "Register",
    data(){
        return{
            name: "",
            password: "",
            passwordcheck: "",
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
            if(!this.passwordcheck){
                this.errors.push("the samepassword is requierd")
            }
            if(this.submit)
            {
                if(this.errors.length === 0){
                    console.log("hello")
                    const newuser = {
                        Name: this.name,
                        Pw: this.password,
                        PwCheck: this.passwordcheck
                    }
                    this.$emit('createaccount',newuser);
                    this.submit = false;
                }
            }

        },
        createAccount(){
           this.submit = true;
        },

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