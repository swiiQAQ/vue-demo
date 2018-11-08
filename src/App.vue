<template>
  <div>
    <ul class="header">
      <li v-for="(item, index) in headerList" v-bind:key="index" class="first-header" @click="openTabHandler(item.name,item.page,item.children)">
        {{item.name}}
        <ul v-if="item.children" class="extend-ul" ref="extendUl">
          <li v-for="(childrenItem, childrenIndex) in item.children" v-bind:key="childrenIndex" @click="openTabHandler(childrenItem.name,childrenItem.page)">
            {{childrenItem.name}}
          </li>
        </ul>
      </li>
    </ul>
    <div>
      <ul class="tab-wrap">
        <template v-for="(item, index) in indexTab">
          <li class="tab-item" v-bind:key="index" :class="currentComponent==item.page?'currentTab':''" @click="openTabHandler(item.name,item.page)">
            {{item.name}}
            <i class="close" v-on:click.stop="closeTabHandler(index)"></i>
          </li>
        </template>
      </ul>
      <div class="tab-content">
        <keep-alive>
          <component :is="currentComponent">
          </component>
        </keep-alive>
      </div>
    </div>
  </div>
</template>

<script>
import index from "./page/Index.vue";
import tab from "./page/Tab.vue";
import cartList from "./page/CartList.vue";
import todoList from "./page/TodoList.vue";

export default {
  name: "app",
  data() {
    return {
      headerList:[
        {
          name: '首页',
          page: 'index'
        },
        {
          name: '选项卡',
          page: 'tab'
        },
        {name:'清单',children:[
          {
            name:'购物清单',
            page: 'cartList'
          },
          {
            name: '任务清单',
            page: 'todoList'
          }
          
        ]}
      ],
      currentComponent: "index",
      indexTab:[
        {
          name: '首页',
          page: 'index'
        }
      ],
    };
  },
  components: {
    index,
    tab,
    cartList,
    todoList
  },
  methods:{
    openTabHandler(name,page,hasChildren){
      if(hasChildren){
        return;
      }
      var temp = this.indexTab;
      var result = temp.find((item)=>{
        if(item.name == name){
          return true;
        }
      })
      if(!result){
        var obj = {
          name: name,
          page: page
        }
        this.indexTab.push(obj);
      }
      this.currentComponent = page; 
    },
    closeTabHandler(index){
      if(!index){return;}
      this.indexTab.splice(index,1);
      this.currentComponent = this.indexTab[index-1].page;
    }
  },

};
</script>

<style>
*{
  list-style: none;
}
.header{
  width: 100%;
  height: 70px;
  background: #333;
  color: #fff;
  /* display: flex; */
  font-size: 20px;
  cursor: pointer;
}
.header li{
  width: 100px;
  text-align: center; 
  height: 100%;
  line-height: 70px;
  display: inline-block;
}
.extend-ul{
  display: none;
  background: #333;
  position: absolute;
  z-index: 2;
}
.extend-ul li{
  display: block;
}
.tab-wrap{
  width: 100%;
  border-bottom: 1px solid #eaeaea;
  margin-top: 50px;
  padding-left: 50px;
}
.tab-item{
  min-width: 100px;
  padding: 0 30px;
  border-top: 1px solid #1abc9c;
  border-left: 1px solid #1abc9c;
  border-right: 1px solid #1abc9c;
  height: 40px;
  display: inline-block;
  margin-left: 15px;
  text-align: center;
  line-height: 40px;
  font-size: 18px;
  position: relative;
  cursor: pointer;
}
.close::after{
  content: 'x';
  position: absolute;
  width: 12px;
  right: 5px;
  line-height: 40px;
  top:0;
}
.currentTab{
  background: #1abc9c;
  color: #fff;
}
.tab-content{
  padding: 50px;
}
.first-header:hover ul{
  display: block;
}
</style>
