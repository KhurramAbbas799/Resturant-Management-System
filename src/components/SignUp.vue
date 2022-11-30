<template>
<h1>Sign Up</h1>


 <div class="register">
<input type="text"  v-model="name"     placeholder="enter name" />
<input type="text"   v-model="email"            placeholder="enter email" />
<input type="password" v-model="password"            placeholder="enter password" />
<button  v-on:click="signUp" >   Sign Up</button>
<p>
<router-link to="/LogIn">   Login      </router-link>            
   </p>

</div>

</template>


<script>
import axios from 'axios'

export default {
    name : 'SignUp',
    data()
    {
        return{
            name:'',
            email:'',
            password:''
        }
    },
    methods:{
       async signUp()
        {
            console.warn("signUp", this.name, this.email, this.password) 
            let result = await axios.post("http://localhost:3000/users",{
                name: this.name,
                email: this.email,
                password: this.password

            }) ;
            console.warn(result);
            if( result.status==201  )
            {
                localStorage.setItem("user-info",JSON.stringify(result.data))
                this.$router.push({name:'HomePage'})
            }
      
        }
    },
    mounted()
    {
        let user =localStorage.getItem('user-info');
        if (user)
        {
            this.$router.push({name:'HomePage'})
        }
    }
}
</script>

<style>

</style>