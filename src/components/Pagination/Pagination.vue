<template>
    <ul class="pagination">
        <li :class="{ disabled:currentPage === 1}"
            @click="setCurrentPage('reduce')"
        ><<</li>
        <li :class="{ disabled:currentPage === 1}"
           @click="setCurrentPage(1)">首页</li>
        <li  v-for="list in pageList"
             :class="{ active:list.value === currentPage }"
             @click="setCurrentPage(list.value)"
        >{{ list.text }}</li>
        <li :class="{ disabled:currentPage === pageNum}"
            @click="setCurrentPage(pageNum)">尾页</li>
        <li :class="{ disabled:currentPage === pageNum}"
            @click="setCurrentPage('add')"
        >>></li>
    </ul>
</template>
<script>
    export default {
        name: 'Pagination',
        props: {
            pageSize:{
                type: Number,
                default: 2
            },//一页多少条数据
            total:{
                type: Number,
                default: 12
            }//总页数
        },
        data(){
            return {
                currentPage: 1
            }
        },
        computed:{
            pageList:function () {
                var list = [
                    {text:1,value:1},
                    {text:2,value:2},
                    {text:3,value:3},
                    {text:4,value:4},
                    {text:'...',value:5},
                    {text:6,value:6}
                ];
                return list;

            },
            pageNum:function () {
                return Math.ceil( this.total / this.pageSize)
            }
        },
        methods:{
            setCurrentPage:function (value) {
                if(value === 'add'){
                    //增
                    this.currentPage < this.pageNum ? this.currentPage++ : this.pageNum;
                }else if(value === 'reduce'){
                    //减
                    this.currentPage > 1 ? this.currentPage-- : 1;
                }else{
                    this.currentPage = value;
                }
            }
        }

    }

</script>
<style scoped lang="less">
    .pagination{
        text-align: center;
        li{
            list-style: none;
            display: inline-block;
            width: 40px;
            height: 40px;
            line-height: 40px;
            margin-right:15px;
            background: #fff;
            border: 1px solid #ebebeb;
            color: #333;
            margin-left: -1px;
            font-size: 14px;
            cursor: pointer;
            &:hover{
                border-color: #6da8f2;
            }
            &.active{
                background: #6da8f2;
                color: #fff;
            }
            &.disabled{
                color: #d8d8d8;
                cursor: not-allowed;
                background-color: #fff;
                border-color: #d8d8d8;
            }
            &.disabled:hover{
                border-color: #d8d8d8;
            }
        }
    }
</style>