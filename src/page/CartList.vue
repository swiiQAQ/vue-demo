<template>
    <div>
        <header class="cartList-header">购物清单</header>
        <div class="list-wrap">
            <ul class="table-menu">
                <li>
                    <label class="checkBox" :class="{'checkedAll':checkedAll}" @click="checkAllHandler"></label>
                    全选
                </li>
                <li>商品</li>
                <li>数量</li>
                <li>单价</li>
                <li>金额</li>
                <li>操作</li>
            </ul>
            <ul v-for="(item, index) in cartList" v-bind:key="index" class="cartItem">
                <li>
                    <label class="checkBox" :class="{'checkedStatus':item.checked}" @click="item.checked=!item.checked"></label>
                </li>
                <li>
                    <img :src="item.img" />
                    <div class='goodDescription'>
                        <p>{{item.goodsName}}</p>
                        <p>{{item.goodsId}}</p>
                    </div>
                </li>
                <li>
                    <numSelect :index='index' :num='item.num' v-on:increase="increaseHandler" v-on:decrease="decreaseHandler"></numSelect>
                </li>
                <li>
                    ￥{{item.price}}
                </li>
                <li>
                    ￥{{item.price*item.num}}
                </li>
                <li @click='deleteItem(index)'>
                    删除
                </li>
            </ul>
        </div>
        <div class="cartList-footer">
            <span @click='deleteCheckedItem'>删除所选商品</span>
            <div>
                <span>{{count}}件商品总计：</span>
                <span>￥{{amount}}</span>
                <span class="goToPay">去结算</span>
            </div>
        </div>
    </div>
</template>


<script>
import numSelect from '../components/NumSelect.vue';

export default {
    name:'cartList',
    components:{
        numSelect
    },
    data(){
        return{
            cartList:[
                {
                    img: 'http://pic.banggo.com/sources/images/goods/MB/661541/661541_00.jpg?x-oss-process=image/resize,m_fill,w_350/quality,Q_50',
                    price: 100,
                    num:1,
                    goodsName:'METERSBONWE 男潮流落肩MA-1空军茄克',
                    goodsId: 23847,
                    checked: false,
                },
                {
                    img: 'http://pic.banggo.com/sources/images/goods/MC/540633/540633_00.jpg?x-oss-process=image/resize,m_fill,w_300,h_410',
                    price: 100,
                    num:1,
                    goodsName:'METERSBONWE 男潮流落肩MA-1空军茄克',
                    goodsId: 23847,
                    checked: false,
                },
                {
                    img: 'http://pic.banggo.com/sources/images/goods/MB/716042/716042_00.jpg?x-oss-process=image/resize,m_pad,w_500,h_500',
                    price: 100,
                    num:1,
                    goodsName:'METERSBONWE 男潮流落肩MA-1空军茄克',
                    goodsId: 23847,
                    checked: false,
                },
            ]
        }
    },
    computed:{
        count:function(){
            var i = 0;
            this.cartList.forEach(function(item) {
                if (item.checked == true){
                    i = i + item.num
                }
            }, this);
            return i;
        },
        amount:function(){
            var amount = 0;
            this.cartList.forEach(function(item) {
                if (item.checked == true){
                    amount = amount + item.price*item.num;
                }
            }, this);
            return amount;
        },
        checkedAll:function(){
            var bool = true;
            this.cartList.forEach((item,index)=>{
                bool = bool && item.checked;
            });
            return bool;
        }
    },
    methods:{
        increaseHandler(index){
            this.cartList[index].num++;
        },
        decreaseHandler(index){
            this.cartList[index].num--;
        },
        checkAllHandler(){
            // this.checkedAll = !this.checkedAll;
            if(!this.checkedAll){
                this.cartList.forEach((item)=>{
                    item.checked = true
                });
            }
            else{
                this.cartList.forEach((item)=>{
                    item.checked = false
                });
            }
        },
        deleteItem(index){
            this.cartList.splice(index,1);
        },
        deleteCheckedItem(){
            this.cartList = this.cartList.filter((item)=>{
                return item.checked == false
            })
        }
    }
}
</script>
<style>
    .checkBox{
        width: 16px;
        height: 16px;
        border: 1px solid #1abc9c;
        border-radius: 50%;
        position: relative;
        box-sizing: border-box;
        display: inline-block;
    }
    .checkBox.checkedStatus::after, .checkBox.checkedAll::after{
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
    .list-wrap{
        width: 100%;
    }
    .table-menu{
        display: flex;
        border-bottom: 1px solid #eaeaea;
        height: 40px;
        line-height: 40px;
    }
    .table-menu li{
        flex-grow: 1;
        text-align: center;
    }
    .table-menu li:first-child{
        flex-grow: 0;
        width: 100px;
    }
    .table-menu li:nth-child(2){
        flex-grow: 0;
        width: 400px;
    }
    .cartList-header{
        background: #1abc9c;
        height: 50px;
        color: #fff;
        padding-left: 40px;
        line-height: 50px;
        font-size: 16px;
    }
    .cartItem{
        display: flex;
        height: 100px;
    }
    .cartItem li{
        display: flex;
        flex-grow: 1;
        justify-content: center;
        align-items: center;
    }
    .cartItem li:first-child{
        flex-grow: 0;
        width: 100px;
    }
    .cartItem li:nth-child(2){
        flex-grow: 0;
        width: 400px;
        justify-content: flex-start;
    }
    .cartItem img{
        width: 60px;
        height: 60px;
    }
    .goodDescription{
        margin-left: 20px;
    }
    .cartList-footer{
        display: flex;
        justify-content: space-between;
        width: 100%;
        background: #eaeaea;
        height: 50px;
        line-height: 50px;
    }
    .cartList-footer span:first-child{
        margin: 0 20px;
    }
    .goToPay{
        margin-left: 30px;
        width: 80px;
        background: #1abc9c;
        color: #fff;
        display: inline-block;
        text-align: center;
    }
    *{
        box-sizing: border-box;
    }
</style>

