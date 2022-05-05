<template>
    <div class="sign">
        <vue-esign ref="esign" class="signPanel" :width="800" :height="300" :isCrop="isCrop" :lineWidth="lineWidth" :lineColor="lineColor" v-model:bgColor="bgColor" />
    </div>
    <div class="signBtn">
        <button @click="handleReset">清空画板</button> 
        <button @click="handleGenerate">生成图片</button>
    </div>
    <div v-if="resultImg" class="signImg">
        <img :src="resultImg" alt="">
    </div>
</template>

<script>
import vueEsign from 'vue-esign'
export default {
    components: {
        vueEsign
    },
    data () {
        return {
            lineWidth: 6,
            lineColor: '#000000',
            bgColor: '',
            resultImg: '',
            isCrop: false
        }
    },
    methods: {
        handleReset () {
            this.$refs.esign.reset()
        },
        handleGenerate () {
            this.$refs.esign.generate().then(res => {
            this.resultImg = res
            }).catch(err => {
            alert(err) // 画布没有签字时会执行这里 'Not Signned'
            })
        }
    }
}
</script>

<style>
.sign{
    display: flex;
    justify-content: center;
}
.signPanel{
    margin: 10px 0;
    border: 2px solid #ccc;
}
.signBtn button{
    color: #fff;
    height: 40px;
    width: 100px;
    font-size: 14px;
    margin-right: 10px;
    outline: none;
    border-radius: 4px;
    background: #f60;
    border: 1px solid transparent;
}
.signImg{
    margin: 10px auto;
    width: 800px;
    border: 1px solid #ccc;
}
</style>