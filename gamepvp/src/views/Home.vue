<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <div v-if="createaccount">
      <register v-on:createaccount ="createAccount" />
    </div>
    <div v-else>
      <Login v-on:Login="LoginUser" v-on:createaccount="wanttocreateaccount"  />
    </div>
    <input type="text" v-model="name">
    <p>user name = {{this.test}}</p>
  </div>
</template>

<script>
// @ is an alias to /src
import Login from '../components/Login'
import axios from 'axios'
import register from '../components/Register'

export default {
  name: 'Home',
  components: {
    Login,
    register
  },
  data()
  { return{
      //testdata
      user: [],
      test:[],

      //nav data
      createaccount: false,

      //user data
      id : null,
      name: '',
      characters: [],

      //send data
      LoginViewModel:{
        Name:'',
        Pw: ''
      },

      registreerViewModel:{
        Name: '',
        Pw: '',
        PwCheck: ''

      },
      
      
    }
  },
  methods: {
    LoginUser(login)
    {
      //this.LoginViewModel = new this.LoginViewModel();
      this.LoginViewModel.Name = login.Name;
      this.LoginViewModel.Pw = login.Pw
      //this.$router.push('/about')
      axios.post('https://localhost:44369/Login/Login', this.LoginViewModel)
            .then(res => {
              console.log("User: " + res.data);
              this.user = res.data;
              this.id = res.data.id
              this.name = res.data.name
            })
      .catch(err => console.log(err))
    },

    wanttocreateaccount(){
      this.createaccount = true;
    },

    createAccount(newuser){
      this.registreerViewModel.Name = newuser.Name;
      this.registreerViewModel.Pw = newuser.Pw;
      this.registreerViewModel.PwCheck = newuser.PwCheck
      //this.$router.push('/about')
      axios.post('https://localhost:44369/Login/Registreer', this.registreerViewModel)
            .then(res => {
              console.log("User: " + res.data);
              this.user = res.data;
              this.id = res.data.id
              this.name = res.data.name
            })
      .catch(err => console.log(err))

    }
    
  },
  created(){
    //axios.defaults.headers.common['Access-Control-Allow-Origin'] = '*';
    axios.get('https://localhost:44369/Battle/LookForBattle/2')
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


