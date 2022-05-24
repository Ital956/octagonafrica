<template>
<img class="logo" src="../assets/logo.png">
<h1>Sign Up</h1>
<div class="register">
    <input type="text"  v-model="firstname" placeholder="Enter First Name"/>
    <input type="text"  v-model="lastname" placeholder="Enter Last Name"/>
    <input type="text"  v-model="email" placeholder="Enter email"/>
    <input type="Password"  v-model="password" placeholder="Enter Password"/>
    <button v-on:click="SignUp">Sign Up</button>

</div>
</template>
<script>
import axios from 'axios'
export default {
    name : 'SignUp',
    data()
    {
        return  {
            firstname:'',
            lastname:'',
            email:'',
            password:''
            
        }
    },
    methods:{
        async SignUp()
        {
            let result = await axios.post("http://localhost:3000/users",{
                email:this.email,
                password:this.password,
                firstname:this.firstname,
                lastname:this.lastname
            });
            console.warn(result);
            if(result.status==201)
            {
                localStorage.setItem("user-info",json.stringify(result.data))
                this.$router.push({name:'Home'})
            }
        }
    },
    mounted()
    {
        let user=localStorage.getItem("user-info")
        if(user)
        {
            this.$router.push({name:'Home'})
        }
    }
}
</script>
<style>
.logo{
    width: 200px;
}
.register input{
    width: 330px;
    height: 70px;
    padding-left: 20px;
    display: block;
    margin-left: auto;
    margin-bottom: 30px;
    margin-right: auto;
    border: 1px solid skyblue;
}
.register button{
    width: 330px;
    height: 70px;
    cursor: pointer;
    background-color: skyblue;
    color: white;
    border: 1px skyblue;
}
</style>