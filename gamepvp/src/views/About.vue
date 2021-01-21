<template>
  <div class="about">
    <h1>This is an about page</h1>
    <p> thisbattle : {{battle}} </p>
    <User />
  </div>
</template>

<script>
import User from  '../components/User'
import axios from "axios"
export default {
  data ()
  {return{
    battle:[]
    }
  },
  components:{
    User
  },
  methods:{

  },
  created(){
    //axios.defaults.headers.common['Access-Control-Allow-Origin'] = '*';
    axios.get('https://localhost:44369/Battle/LookForBattle/1')
    .then(res => this.battle = res.data)
    .catch(err=> console.log(err));
    console.log(123)
  }
}
</script>
