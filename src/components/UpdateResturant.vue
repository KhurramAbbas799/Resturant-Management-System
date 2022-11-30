<template>
<HeaderPage />
<h1>hello user welcome on update resturant  page</h1>
<form class="add">
<input type="text" placeholder="enter name" v-model ="resturant.name" name="name" />
<input type="text" placeholder="enter address" v-model ="resturant.address"  name="address" />
<input type="text" placeholder="enter contact"  v-model="resturant.contact" name="contact" />
<button type="button" v-on:click="updateResturant">    update new resturant</button>
</form>
</template>

<script>
import HeaderPage from './HeaderPage.vue';
import axios from 'axios';
export default {
    name: 'UpdateResturant',
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
       async updateResturant()
        {
            //console.warn("function called",this.resturant)
             const result = await axios.put("http://localhost:3000/resturant/"+this.$route.params.id,{
                name:this.resturant.name,
                 address:this.resturant.address,
                 contact:this.resturant.contact,

            });
            if(result.status==200)
            {
                this.$router.push({name:'HomePage'});
            
            }
        }
    },
   async mounted() {
        let user = localStorage.getItem('user-info');
        if (!user) {
            this.$router.push({
                name: 'SignUp'
            })
        }
        const result =await axios.get("http://localhost:3000/resturant/"+this.$route.params.id);
       // console.warn(this.$route.params.id)
       //console.warn(result.data)
       this.resturant=result.data
    }


};
</script>
