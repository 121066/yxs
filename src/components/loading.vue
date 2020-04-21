<template>

    <div class="load" v-if="ys">
    <div class="loading"></div>
    <span>{{msg}}</span>
    <!-- <span >{{is}}</span> -->
    <!-- <span v-for="item in is" :key="item.id">
        <span>{{item.name}}</span>
    </span> -->
   <button @click="yxs">红尘雪</button>
</div>
 
</template>
<script>
export default {
    props:["msg"],
data(){
    return{
        //is:is,
  ys:false,
  db:'大家都是一样的'
    }
},
created(){
    console.log('33')
console.log(this.msg)
},
methods:{
    yxs(){
        console.log('232')
        this.$emit('yxs',this.db)
        console.log(this.db)
    }
},
mounted(){
   setTimeout(()=>{
       this.ys=true
   },500)
    setTimeout(()=>{
        this.ys=false
    },5000)
}
}
</script>
<style lang="less" scoped>
  .load {
            width: 100%;
            height: 100%;
            background: rgba(99, 99, 102, 0.774);
        }
        
        .loading {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) rotate(75deg);
            width: 15px;
            height: 15px;
            /* background: purple; */
            transition: all .5s;
        }
        
        .loading::before,
        .loading::after {
            content: "";
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 15px;
            height: 15px;
            border-radius: 15px;
            /* background: black; */
            animation: loading 1.5s infinite linear;
        }
        
        .loading::before {
            box-shadow: 15px 15px #e77f67, -15px -15px #778beb;
        }
        
        .loading::after {
            box-shadow: 15px 15px red, -15px -15px pink;
            transform: translate(-50%, -50%) rotate(90deg);
        }
        
        @keyframes loading {
            50% {
                height: 45px;
            }
        }
        span{
            position: absolute;
            width: 40px;
            height: 20px;
            color: aqua;
            font-size: 12px;
            top: 55%;
            left: 50%;
            font-weight: 600;
            transform: translate(-50%, -50%);
        }
        
</style>