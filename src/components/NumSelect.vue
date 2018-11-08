<template>
    <div class="numSelectWrap">
        <span @click="decrease">-</span>
        <input type="text" :value='num'/>
        <span @click="increase">+</span>
    </div>
</template>


<script>

export default {
    props: ['num','index'],
    methods:{
        increase(){
            this.$emit('increase',this.index);
        },
        decrease(){
            this.$emit('decrease',this.index);
        }
    }
}
</script>
<style>
*{
    box-sizing: border-box;
}
    .numSelectWrap{
        display: flex;
        border: 1px solid #1abc9c;
        border-radius: 3px;
        height: 22px;
        text-align: center;
    }
    .numSelectWrap span{
        width: 30px;
        height: 20px;
        background: #f1f1f1;
        display: inline-block;
        background: #1abc9c;
        color: #ffffff;
        cursor: pointer;
    }
    .numSelectWrap input{
        width: 44px;
        height: 20px;
        border: none;
        border-left: 1px solid #eaeaea;
        border-right: 1px solid #eaeaea;
        text-align: center;
        outline: none;
    }
</style>