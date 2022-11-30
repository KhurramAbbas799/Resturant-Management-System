<template>
<HeaderPage />
<h1>hello user welcome on add resturant page</h1>
<form class="add">
<input type="text" placeholder="enter name" v-model ="resturant.name" name="name" />
<input type="text" placeholder="enter address" v-model ="resturant.address"  name="address" />
<input type="text" placeholder="enter contact"  v-model="resturant.contact" name="contact" />
<button type="button" v-on:click="addResturant">    add new resturant</button>
</form>
</template>
 
<script>
import axios from 'axios';
import HeaderPage from './HeaderPage.vue';
export default {
    name:'AddResturant',
    components: {
        HeaderPage
    },
    data()
    {
        return  {
            resturant:{
                name:'',
                address:'',
                contact:''
            }
        }
    },
    methods:{
      async  addResturant()
        {
            console.warn(this.resturant)
            const result = await axios.post("http://localhost:3000/resturant",{
                name:this.resturant.name,
                 address:this.resturant.address,
                 contact:this.resturant.contact,

            });
            if(result.status==201)
            {
                this.$router.push({name:'HomePage'});
            
            }
            console.warn("result",result)
        }
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if (!user) {
            this.$router.push({
                name: 'SignUp'
            })
        }
    }
};
</script>
