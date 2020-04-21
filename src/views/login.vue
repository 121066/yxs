<template>
<div>
    <!-- <div class="box">
        <p> <button type="text">登录</button> <button type="text">注册</button> </p>
        <input type="text" placeholder="请输入用户名" class="login" value="" v-model="username">
        <input type="password" placeholder="请输入密码" class="main" value="" v-model="password">
        <span><button @click="Login">登录</button> </span>
    </div> -->
<div class="box">
    <input type="text" placeholder="请输入用户名/手机号" v-model="username">
    <input type="password" placeholder="请输入密码" v-model="password">
    <button class="btn" @click="add">登录</button>
    <button class="btn1" @click="Login">注册</button>
</div>
</div>
</template>
<script>
export default {
   // name:'login',
    data(){
        return{
            username:'',
            password:''
        }
    },
    created(){

    },
    methods:{
        Login(){ 
            this.$axios.post('/getuser',{user:this.username,password:this.password}).then(res=>{
              //  console.log(res)
              //  alert(res)
                if(res.data.err_code==1){
                  //  alert('121')
                    this.$axios.post('/user',{user:this.username,password:this.password}).then(res=>{
                        if(res.data.err_code==1)return  this.$toast('注册失败')
                        window.sessionStorage.setItem('token',res.data.jwt)
                        this.$router.push('/home')
                    })
                }
            })
        },
        add(){
            this.$axios.post('/users/login',{user:this.username,password:this.password}).then(res=>{

               if(res.data.err_code!==1){
                    this.$toast('登陆成功')
                    window.localStorage.setItem('username',this.username)
                window.sessionStorage.setItem('token',res.data.jwt)
                this.$router.push('/home')
               }else{
                   console.log('密码不正确',this)
                   alert('账号或密码不正确')
                   // $toast('账号或密码不正确')
               }
            })
        }
    }
}
</script>
<style lang="less" scoped>
div{
    background-color: #eee;
    background: url('../assets/logins.png') no-repeat;
    background-size: 100% 100%;
    height: 100%;
    width: 100%;
    margin-bottom: 50px;
    padding: 0;
    position: fixed;
    top: 0;
    bottom: -50px;
    z-index: 1111;
}
.box{
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    >input{
   background-color: transparent;
   //opacity: .1;
    border: 0;
    color: #fff;
   // border-bottom: 1px solid #fff;
   
}
>button{
   // justify-content: space-between;
    background: transparent;
    border: 0;
    color: #fff;
    width: 80%;
    height: 50px;
   // border: 1px solid #fff;
    border-radius: 25px;
}
 .btn{
        position: absolute;
        top: 60%;
        background-color: #35c88c;
        left: 10%;
        font-size: 16px;
    }
    .btn1{
        position: absolute;
        top: 70%;
        font-size: 18px;
        left: 10%;
        border: 1px solid #fff;
    }
input:nth-child(1){
    position: absolute;
    top: 38%;
    width: 90%;
    left: 5%;
}
input:nth-child(2){
    position: absolute;
    top: 47%;
    width: 90%;
    left: 5%;
}
  input::-webkit-input-placeholder{
        color: #fff!important;
        //font-size: 30px;
    }
   
}

</style>