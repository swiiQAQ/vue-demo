<template>
    <div>
        <h1>todolist</h1>
        <h2>添加小目标</h2>
        <input class="active" v-model='todos' type='text' @keyup.enter="addList"/>
        <p>共有个{{task.length}}目标，已完成，还有条未完成</p>
        <div class="filterWrap" >
            <div v-for="(item,index) in filter" :key='index'>
                <label class="filterBox" :class="filterIndex==index? 'checkedStatus':''" @click='filterChangeHandler(index)'></label>
                <span>{{item}}</span>
            </div>
        </div>
        <div class="todoList">
            <div v-for="(item, index) in newList" :key='index' >
                <label class="checkList" :class="{checkedStatus:item.done}" @click='item.done = !item.done'></label>
                <input type="text" class="" v-model='item.name' :class='{active: selectedIndex === index}' @focus='selectedIndex = index' @blur='selectedIndex = ""'/>
            </div>
        </div>
    </div>
    
</template>


<script>

export default {
    name:'todoList',
    watch:{
        task(val){
          this.newList = this.task;
        }
    },
    data(){
        return{
            filterIndex: 0,
            filter:['所有目标','已完成目标','未完成目标'],
            task:[],
            newList: [],
            todos:'',
            selectedIndex: ''
        } 
    },
    methods:{
        addList(){
            var obj={
                name: this.todos,
                done: false
            }
            this.task.push(obj);
            this.todos = '';
        },
        filterChangeHandler(index){
            this.filterIndex = index;
            if(index == 1){
                this.newList = this.task.filter((item)=>{
                    return item.done
                })
            }
            else if(index == 2){
                this.newList = this.task.filter((item)=>{
                    return !item.done
                })
            }
            else{
                this.newList = this.task
            }
        }
    }
}
</script>
<style>
    input.active{
        padding-left: 8px;
        border: none;
        border: 2px solid #1abc9c!important;
        border-radius: 3px;
        height: 38px;
        width: 300px;
        margin: 20px 0;
    }
    .filterWrap{
        display: flex;
    }
    .filterWrap div{
        display: flex;
        align-items: center;
    }
    .filterWrap label{
        margin-right: 8px;
    }
    .filterWrap span{
        margin-right: 20px;
    }
    .filterBox{
        width: 16px;
        height: 16px;
        border: 1px solid #1abc9c;
        border-radius: 50%;
        position: relative;
        box-sizing: border-box;
        display: inline-block;
    }
    .filterBox.checkedStatus::after, .filterBox.checkedAll::after{
        content: '';
        position: absolute;
        left: 50%;
        margin-left: -5px;
        top: 50%;
        margin-top: -5px; 
        width: 10px;
        height: 10px;
        border-radius: 50%;
        background: #1abc9c;
    }
    .checkList{
        width: 10px;
        height: 10px;
        border: 1px solid #1abc9c;
        position: relative;
        box-sizing: border-box;
        display: inline-block;
        margin-right: 10px;
    }
    .checkList.checkedStatus{
        background: #1abc9c;
    }
    .todoList{
        font-size: 20px;
    }
    .todoList input{
        border: none;
    }
</style>

