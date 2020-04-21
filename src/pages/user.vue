<template>
<div>
   <div class="box">
       <img src="../assets/tx.jpg" alt="" class="ims"/>
       <!-- <div class="ps"> -->
           <p>{{username}}</p>
           <span @click="detail">注销</span>
       <!-- </div> -->
       <div class="ps">
           <!-- <div class="main"> -->
               <span>会员权益</span>
           <span>现在下单还有返利哦</span>
           <span>开通会员</span>
           <!-- </div> -->
           <div class="money">
           <p class="spn">我的钱包</p>
           <p class="spn1">进入钱包</p>
       </div>
       <div class="mon">
           <ul>
               <li>
                   <p>119￥</p><p>账户余额</p>
               </li>
               <li> <p>$10.00</p><p>平台返现</p></li>
               <li> <p>7</p><p>优惠券</p></li>
               <li> <p>455</p><p>金币</p></li>
           </ul>
       </div>
       <div class="logi">
           <img src="../assets/tx.jpg" alt=""/>
           <p class="p1">已发出</p>
           <p class="p2">包裹经顺丰快递发出</p>
       </div>
       <div class="order">
           <ul>
               <li>
                   <img src="../assets/代付款.png" alt="">
                   <p>待付款</p>
               </li>
               <li><img src="../assets/待收货.png" alt="">
                   <p>待收货</p></li>
               <li><img src="../assets/待评价.png" alt="">
                   <p>待评价</p></li>
               <li><img src="../assets/退款收货.png" alt="">
                   <p>退货退款</p></li>
               <li><img src="../assets/全部订单.png" alt="">
                   <p>全部订单</p></li>
           </ul>
       </div>
       <div class="plar">
           <ul>
               <li>
                    <img src="../assets/我喜欢的.png" alt="">
                   <p>我喜欢的</p>
               </li>
               <li> <img src="../assets/我的关注.png" alt="">
                   <p>我的关注</p></li>
               <li> <img src="../assets/商品浏览.png" alt="">
                   <p>商品浏览</p></li>
               <li style="z-index:-12;"> <img src="../assets/我的签到.png" alt="">
                   <p>我的签到</p></li>
               <li> <img src="../assets/我的话题.png" alt="">
                   <p>我的话题</p></li>
               <li> <img src="../assets/积分商城.png" alt="">
                   <p>积分商城</p></li>
               <li> <img src="../assets/我的活动.png" alt="">
                   <p>我的活动</p></li>
               <li> <img src="../assets/会员频道.png" alt="">
                   <p>会员频道</p></li>
           </ul>
       </div>
       </div>
       
   </div>
</div>
</template>
<script>
export default {
    data(){
        return{
            username:'',
        }
    },
    created(){
        let user=[]
        if(window.localStorage.getItem('username')||user){
            this.username=window.localStorage.getItem('username')
        }
    },
    methods:{
        detail(){
            window.sessionStorage.clear('token')
            window.localStorage.clear('username')
            this.$router.push('/login')
        }
    }
}
</script>
<style lang="less" scoped>
div{
    height: 100%;
    width: 100%;
    //background: url('../assets/user.png') no-repeat;
    background: url('../assets/user.png')no-repeat;
    background-size: 100% 100%;
    position: fixed;
    top: 0;
    z-index: -11;
    //z-index: 1111;
    bottom: -50px;
}
.box{
    display: flex;
    width: 100%;
    flex-direction: column;
   // justify-content: ;
  // align-items:flex-start ;
  //z-index: 1122;
   
    >.ims{
        position: absolute;
        top: 9%;
        left: 8%;
        width: 50px;
        height: 50px;
        border-radius: 25px;
      //  border: 1px solid #fff;
        //z-index: 11;
    }
    >p{
        position: absolute;
        top: 10%;
        left: 23%;
        color: #fff;
       // display: inline-block;
       // flex: 1;
       //z-index: 11;
    }
    >span{
        position: absolute;
        top: 13%;
        left: 23%;
        color: #fff;
       // z-index: 11;
    }
    .ps{
        // position: absolute;
        // top: 10%;
        width: 100%;
        height: 100%;
       display: flex;
       flex-direction: row;
       flex-flow: wrap;
       justify-content: flex-end;
       margin-bottom:1px; 
       //z-index: 11;
    }
    .ps span:nth-child(3){
        position: absolute;
             width: 60px;
             color: #fff;
             font-size: 14px;
             top: 20.7%;
             right: 10%;
            // flex: 1;
        }
        .ps span:nth-child(1){
            position: absolute;
            top: 20%;
            left: 20%;
            color: #a78651;
        }
        .ps span:nth-child(2){
            position: absolute;
             top: 23%;
             left: 20%;
             font-size: 12px;
             color: #976a2e;
        }
   .ps .money{
      // position: absolute;
      width: 100%;
        display: flex;
        flex-direction: row;
        justify-content: space-evenly;
        >.spn{
            position: absolute;
            top: 29%;
            left: 10%;
            font-size: 18px;
        }
        >.spn1{
            position: absolute;
            top: 29%;
            right: 10%;
        }
    }
    .ps .mon{
        position: absolute;
        top: 34%;
        width: 100%;
        height: 85px;
        background-color: #fff;
        background: transparent;
       // border: 1px solid red;
        // display: flex;
        // flex-direction: row;
        // justify-content: space-evenly;
        // flex-wrap: wrap;

        ul{
            width: 100%;
            height: 100%;
            //float: left;
            box-sizing: border-box;
        }
        >ul li{
            //align-items: center;
            float: left;
            margin: 0;
            padding: 0;
            //flex: 1;
            width: 25%;
            height: 100%;
           // border: 1px solid pink;
            >p{
                margin: 10px 0 0 0;
                color: #000;
            }
            p:nth-child(1){
                font-size: 18px;
            }
            p:nth-child(2){
                font-size: 12px;
                font-weight: 700;
            }
        }
    }
    .ps .logi{
        width: 100%;
        height: 50px;
      //  border: 1px solid red;
        background: transparent;
        position: absolute;
        top: 48%;
        >img{
            position: absolute;
            top:5%;
            left: 5%;
            width: 40px;
            height: 40px;
        }
        >p{
           // display: inline;
            margin: 0;
        }
       .logi>.p1{
            position: absolute;
            width: 40px;
            top: 0%;
            left: 10%;
            margin: 0;
           // display: block;
        }
        .logi>.p2{
            position: absolute;
            width: 100px;
            top: 10%;
            left: 0;
            margin: 0;
        }
    }
    .ps .order{
        width: 100%;
        height: 85px;
        position: absolute;
        top: 55%;
        background: transparent;
      //  border: 1px solid red;
        >ul {
            width: 100%;
            height: 100%;
            box-sizing: border-box;
        }
        >ul li{
            float: left;
            height: 100%;
            width: 20%;
          //  border: 1px solid pink;
            padding: 15px 0 0 0;
            >img{
                width: 30px;
                height: 30px;
            }
        }
    }
    .ps .plar{
        width: 100%;
        height: 118px;
        position: absolute;
        top: 75%;
        background: transparent;
        >ul{
            width: 100%;
            height: 100%;
            box-sizing: border-box;
        }
        >ul li{
            float: left;
            height: 50%;
            width: 25%;
          //  border: 1px solid pink;
            >img{
                width: 30px;
                height: 30px;
               // padding: 5px 0 0 0;
            }
        }
    }
}
</style>