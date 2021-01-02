<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <Login v-on:Login="LoginUser" />
    <input type="text" v-model="LoginViewModel.name">
    <p>user name = {{this.test}}</p>
  </div>
</template>

<script>
// @ is an alias to /src
import Login from '../components/Login'
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    Login
  },
  data()
  { return{
    user: [],
      id : null,
      name: '',
      characters: [],
      LoginViewModel:{
        Name:'',
        Pw: ''
      },
      test:[]
    }
  },
  methods: {
    LoginUser(login)
    {
      //this.LoginViewModel = new this.LoginViewModel();
      this.LoginViewModel.Name = login.Name;
      this.LoginViewModel.Pw = login.Pw
      //this.$router.push('/about')
      axios.get('https://localhost:44369/Login/Login', this.LoginViewModel)
            .then(res => {
              console.log("User: " + res.data);
              this.user = res.data;
              this.id = res.data
              this.name = res.data.name
            })
      .catch(err => console.log(err))
    },
  },
  created(){
    //axios.defaults.headers.common['Access-Control-Allow-Origin'] = '*';
    axios.get('https://localhost:44369/Login/GetAll')
    .then(res => this.test = res.data)
    .catch(err=> console.log(err));
    console.log(123)
    }
}
</script>

<style scoped>
body{
  background-color: #ededed;
}

</style>


