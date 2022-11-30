<template>
<HeaderPage />
<h1>hello  {{name}},  Welcome on home page</h1>
<table border="1">
<tr>
<td>id</td>
<td>name</td>
<td>address</td>
<td>contact</td>
<td>actions</td>
</tr>
<tr v-for="item in resturant" :key="item.id" >
 <td>{{item.id}}</td>
 <td>{{item.name}}</td>
 <td>{{item.address}}</td>
 <td>{{item.contact}}</td>
 <td>
 <router-link :to="'/update/'+item.id">  update </router-link>  
 <button v-on:click="deleteResturant(item.id)" >  Delete </button>
    </td>
 </tr>
 </table>
    </template>

<script>
import axios from 'axios';

import HeaderPage from './HeaderPage.vue';
export default {
    name: 'HomePage',
    data()
    {
        return{
             name:'',
            resturant:[],
        }
    },
        components: {
        HeaderPage
    },
    methods:{
     async deleteResturant(id)
      {
        let result=await axios.delete("http://localhost:3000/resturant/"+id);
            if(result.status==200)
      {
           this.loadData()
      }
      },
      async loadData()
      {
        let user = localStorage.getItem('user-info');
       this.name= JSON.parse(user).name
        if (!user) {
            this.$router.push({name: 'SignUp'})
        }
        let result=await axios.get("http://localhost:3000/resturant");
        console.warn(result)
        this.resturant=result.data
      }
    },
    mounted() {
        this.loadData()
      }
};
</script>
<style>
td{
    width: 160px;
    height: 40px;
}

</style>