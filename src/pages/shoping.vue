<template>
    <div class="by">
      
      <div class="main" v-for="item in list" :key="item.id">
          <van-checkbox v-model="$store.getters.getGoodsSelected[item.id]" class="check"
          @click="toggle(item.id,$store.getters.getGoodsSelected[item.id])"
          ref='checkbox'
          ></van-checkbox>
      <img :src="item.banelurl" alt="" class="imgs"/>
      <!-- </template> -->
      <div class="box">
          <p>{{item.goodsname}}</p>
          <span>￥{{item.price}}.00元</span>
          <div class="num1">
 <numbox :goodsid="item.id" :initcount="$store.getters.getGoodsCount[item.id]" style="margin:0;"></numbox>
          </div>
      </div>
      
    <!-- <van-button square type="danger" text="删除" style="height:100%;"/> -->
<div class="side" @click.prevent="remove(item.id)">
删
除
</div>
     </div>
   
<div class="footer">
 <div><van-checkbox  >全选</van-checkbox></div>
 <span>共{{$store.getters.getGoodsCountAndAmount.count}}件</span>
 <button>{{$store.getters.getGoodsCountAndAmount.amount}}元</button>
</div>
    </div>
</template>
<script>
import numbox from '../components/shopingnumbox.vue'
export default {
    data(){
        return{
            checked:true,
           // value:'',
            id:this.$route.query.id||[],
            list:[],
            goodsinfo:{},
            selectedCount:1
        }
    },
    created(){
        this.getlist()
       // this.getadd()
       //console.log(this.$store.getters.getGoodsCount[item.id])
    },
    methods:{
        onClose(clickPosition, instance) {
      switch (clickPosition) {
       // case 'left':
        case 'cell':
        case 'outside':
          instance.close();
          break;
        case 'right':
            console.log('确定删除吗')
        //   Dialog.confirm({
        //     message: '确定删除吗？'
        //   }).then(() => {
        //     instance.close();
        //   });
          break;
      }
    },
    getlist(){
        console.log(typeof this.id)
        //var ids=this.id.split(' ')
        var ids=[]
        this.$store.state.car.forEach(item=>{
            ids.push(item.id)
        })
        console.log(ids)
        this.$axios.post('/goods/detas').then(res=>{
            res.data.message.forEach(item=>{
                ids.forEach(item1=>{
                    if(item.id==item1){
                        return this.list.push(item)
                    }
                })
            })
            console.log(this.list)
        })
    },
    getadd(){
      
    },
    selectedChanged(id,val){
        console.log(val)
        console.log('22')
      //  this.$store.commit('updateGoodsSelected',{id,selected:val})
    },
    toggle(id,val){
        console.log(val)
        //console.log(this.$refs.checkbox[2].value)
        this.$store.commit('updateGoodsSelected',{id,selected:val})
    },
    remove(id){
        console.log(id)
       // console.log(index,'index')
       const obj=[]
       this.list.forEach(item=>{
           if(item.id==id){
               return  this.list.pop(item)
           }
       })
       console.log(obj)
        this.$store.commit('removes',id)
       // this.getlist()
    }
    },
    components:{
        numbox
    }
}
</script>
<style lang="less" scoped>
.by{
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}
 .main{
    //  background:linear-gradient(to right,#fcc);
    background: #fff;
    width: 98%;
    height: 150px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    margin: 5px;
    border: 1px #fff dotted;
    box-shadow: 0px 3px 3px 3px #ccc;
    .check{
        width: 40px;
        height: 40px;
    }
    img{
        width: 100px;
        height: 100px;
    }
    .box{
        display: flex;
        flex: 1;
        flex-direction: column;
        justify-content: space-around;
        
        p{
            text-align: left;
            height: 50px;
            margin: 10px 0 0 0;
        }
        span{
            flex: 30px;
            text-align: left;
            color: #cc0000;
            line-height: 30px;
        }
       .num1{
            flex: 30px;
            text-align: right;
          align-content: flex-end;
        }
    }
    
    .side{
        width: 20px;
        height: 100%;
        line-height: 70px;
        background-color: #ff0000;
    }
}
.footer{
    width: 100%;
    height: 50px;
    background-color: #fff;
    position: fixed;
    bottom: 50px;
    >div{
        position: absolute;
        top: 35%;
    }
    span{
        width: 50px;
        height: 30px;
        position: absolute;
        top: 30%;
        right:  30%;
    }
    button{
        position: absolute;
        top: 20%;
        right: 10%;
        width: 60px;
        border: none;
        color: #fff;
        border-radius: 10px;
        background-color: #cc0000;
    }
}
</style>