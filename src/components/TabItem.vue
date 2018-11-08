<template>
    <div class="tab">
        <div class="tab-car">
            <a class="tab-car-item" v-for="(item, index) in list" v-bind:key="index" @click="tabSelectHandler(index)" v-bind:class="{'selected':showId==index}">
            </a>
        </div>
        <div class="tab-content">
            <div class="tab-content-item" v-for="(item, index) in list" v-bind:key="index" v-show="showId==index">
                {{index}}
            </div>
        </div>
    </div>
</template>

<script>
export default {
  props: ["size"],
  data() {
    return {
      list: this.numToList(this.size),
      showId: 0
    };
  },
  methods: {
    numToList: function(num) {
      var arr = [];
      for(var i=0;i<this.size;i++){
          arr[i] = i
      }
      return arr;
    },
    tabSelectHandler: function(id) {
      this.showId = id;
    }
  },
};
</script>


<style>
*{
    box-sizing: border-box;
}
.tab {
  width: 800px;
  display: flex;
  flex-direction: column;
}
.tab-car {
  display: flex;
}
.tab-car-item {
  background: #1abc9c;
  display: flex;
  flex-grow: 1;
  height: 40px;
  border: 1px solid #eaeaea;
}
.tab-content-item {
  width: 100%;
  height: 400px;
  background: #fff;
  border: 1px solid #eaeaea;
}
.selected {
    background: #fff;
}
</style>

