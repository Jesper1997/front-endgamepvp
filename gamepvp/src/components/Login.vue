<template>
    <form @submit.prevent="loginUser">
        <div>
            <h4>username</h4>
            <input type="text" v-model="name" name="name" placeholder="insery username">
            <h4>password</h4>
            <input type="password" v-model="password" name="password" placeholder="Insert password">
            <br>
            <input type="Submit" value="Login" class="btn">
        </div>
    </form>
</template>

<script>
export default {
    name: "Login",
    data(){
        return{
            name: '',
            password: '',
        }
    },
    methods:{
        loginUser(){
            const login = {
                Name: this.name,
                Pw: this.password
            }
            this.$emit('Login',login);
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
</style>