<template>
  <div>
   <h1>{{yy}}</h1>
    <h2>你好呀</h2>
    <!-- <baidu-map class="map">
    </baidu-map>-->
    <load :msg="msg"  @yxs='change($event)'></load>
    
  </div>
  
</template>
<script>
import load from '@/components/loading.vue'
export default {
  //props: ['is'],
  data() {
    return {
      // is: [
      //   { id: 1, name: '你好' },
      //   { id: 2, name: '不好' }
      // ]
      msg:'你好',
      yy:''
    }
  },
  created(){
    console.log(this.yy)
  },
  methods:{
    change(db){
      console.log('有没有值呀')
      this.yy=db
    }
  },
  components: {
    load
  }
}
</script>
<style lang="less" scoped>
.map {
  width: 100%;
  height: 300px;
}
</style>