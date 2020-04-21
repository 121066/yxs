<template>
<div>
    <input type="text" v-model="int" placeholder="请输入要生成的内容" @blur="delet">
<qrcode :value="value" :size="size" level="H"></qrcode>
</div>
</template>
<script>
import Qrcode from 'qrcode.vue'
export default {
    data(){
        return{
            value:'',
            size:100,
            int:''
        }
        
    },
    methods:{
        delet(){
            //this.int=''
        }
        },
    components:{
        Qrcode
    },
    watch:{
        int(newVal){
            this.value=newVal
        }
    }
}
</script>
<style lang="less" scoped>

</style>