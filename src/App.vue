<template>
  <div id="app">
  <div class="col-xs-6" v-if="x">
  
  <input style="margin-top:10px" class="form-control" type="text" v-model="x.email">
  <input style="margin-top:10px" class="form-control" type="password" v-model="x.password">
  <button style="margin-top:10px" class="btn btn-success" v-on:click="post(x)">submit</button>
  </div>

  <div v-if="resToken">
  {{resToken}}
  </div>

  <div class="text-center text-primary" v-if="data.length<1">
    <h3>Loading....</h3>
  </div>
  <div class="container col-xs-6">

  <table class="table table-striped" v-if="data">
    <tr class="text-center">
      <th>S/R
      </th>
      <th>First Name </th>
      <th>Last Name
      </th> 
    </tr>
    <tr v-for="(x,index) of data">
    <td>{{index +1}}
    </td>
    <td>{{x.first_name}}</td>
      <td>{{x.last_name}}</td>

    </tr>
  </table>
  </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {x:{
   email:"test@gmail.com",
    password : "test"
    },
    data:{},
    resToken:""
    }
      },
      methods:{
        post:function(x){
          this.$http.post('https://reqres.in/api/register',x).then(function(res){
            console.log(res);
            this.resToken = res.data.token;
            console.log(this.resToken);
          })
        },
        get:function(){
          this.$http.get('https://reqres.in/api/users?page=2').then(function(res){
            this.data =  res.data.data;
            console.log(res.data.data);
          },function(error){
            console.log(error);
          })
        }
      },
       beforeMount(){
         this.get();
       }
  }

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
