<template>
<div>
    <!-- <h1>高清图片</h1> -->
    <van-tabs v-model="active" animated @click="goodslist">
  <van-tab v-for="item in this.list" :title="item" :key="item.id">
    <!-- 内容 {{ item.id }} -->
    <div v-for="item in Goods" :key="item.id" class="cards">
        <van-card
  :price="item.price"
  :desc="item.gender==0?'男士':'女生'"
  :title="item.goodsname"
  :thumb="item.banelurl"
@click="goods(item.id)"
>
  <div slot="tags">
    <van-tag plain type="danger">包邮</van-tag>
    <van-tag plain type="danger">退换</van-tag>
  </div>
  <div slot="footer">
    <van-button size="mini">加入购物车</van-button>
    <van-button size="mini" >购买</van-button>
  </div>
</van-card>
    </div>
  </van-tab>
</van-tabs>
</div>
</template>
<script>
export default {
    data(){
        return{
          list:[],
          //  list:['全部','衣服','内衣','女士','男士','儿童'],
            active:'',
            Goods:[],
            id:this.$route.query.id-1||0,
           type:''
        }
    },
    created(){
      this.goodsname()
      this.goodslist(0)
    },
    methods:{
        goodslist(name,title){
        //  console.log(name,title)
           // console.log(name,title)
           // console.log(this.id)
           // let data={type:name||this.id}
          // let data
           if(name){
             console.log(name)
             this.type=name
             // data={type:name}
           }else{
             // data={type:this.id}
            this.type=name||this.id
           }
          // let data={type:name}
         //  console.log(data)
         console.log(this.type)
            this.$axios.post('/goods/list',{type:this.type}).then(res=>{
               // console.log(res)
                this.Goods=res.data.message
                this.Goods.forEach(item=>{
                 // console.log(item.banelurl)
                    // console.log(item.url.split(","))
                    this.Goods.banelurl=item.banelurl.split(' ')
                })
                //console.log(this.Goods)
            })
        },
        goods(id){
          //  console.log(id)
            this.$router.push('/goodsdetail?id='+id)
        },
        goodsname(){
          this.$axios.post('/goods').then(res=>{
           // console.log(res)
            //let goodsA=res.data.message.name
            res.data.message.forEach(item=>{
              this.list.push(item.name)
            })
          })
        }
    },
    watch:{
      type(val,oldVal){
        console.log(val,oldVal)
       // type=val
       this.type=val
      }
    }
}
</script>
<style lang="less" scoped>
.van-card__content{
    text-align: left;
}
.cards{
    border-bottom: 3px solid #ffff00;
}
</style>