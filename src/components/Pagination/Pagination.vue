<!--
说明：分页组件
传参：pageSize（一页多少数据） total（所有的数据）
出参：currentPage（点击的当前页）
-->
<template>
    <ul class="pagination">
        <li :class="{ disabled:currentPage === 1}"
            @click="setCurrentPage('reduce')"
        ><<</li>
        <li :class="{ disabled:currentPage === 1}"
           @click="setCurrentPage(1)">首页</li>
        <li  v-for="list in pageList"
             :class="{ active:list.value === currentPage,point:list.type ==='point'}"
             @click="setCurrentPage(list)"
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
            pageSize:{//一页多少条数据
                type: Number,
                default: 1
            },
            total:{//总条数
                type: Number,
                default: 1
            }
        },
        data(){
            return {
                currentPage: 1,
                pagegroup:5
            }
        },
        computed:{
            pageNum:function () {
                //一共多少页
                return Math.ceil( this.total / this.pageSize)
            },
            pageList:function () {
                let len = this.pageNum,temp = [],list=[];
                if(len <= this.pagegroup){
                    //5页一组，如果页数小于等于不显示点点点
                    while(len--){
                        temp.push({text:this.pageNum - len,value:this.pageNum-len});
                    }
                    return temp;
                }
                while (len--) {
                    temp.push(this.pageNum - len);
                }
                //当前页小于this.pagegroup - 1
                if(this.currentPage < this.pagegroup - 1 ){
                    for(let i = 0; i < this.pagegroup; i++){
                        list.push({text:i+1,value:i+1});
                    }
                    list.push({text:'...',value:this.pagegroup,type:'point'});
                    list.push({text:this.pageNum,value:this.pageNum});
                    return list;
                }
                //第this.pagegroup - 1页
                if(this.currentPage === this.pagegroup - 1){
                    for(let i = 0; i <= this.pagegroup; i++){
                        list.push({text:i+1,value:i+1});
                    }
                    list.push({text:'...',value:this.pagegroup,type:'point'});

                    list.push({text:this.pageNum,value:this.pageNum});

                    /*    temp.forEach((item,i)=>{
                        if(i >= 0 && i <= this.pagegroup){//0-5
                            list.push({text:i+1,value:i+1});
                        }else if(i === this.pagegroup+1){
                            if(i < this.pageNum-2){
                                list.push({text:'...',value:this.pageNum-1,type:'point'});
                            }
                            list.push({text:this.pageNum,value:this.pageNum});
                        }
                    });*/
                    return list;
                }
                // 当前页大于this.pagegroup 并且小于this.pageNum-4
                if(this.currentPage >= this.pagegroup && this.currentPage < this.pageNum-4){
                    list.push({text:1,value:1});
                    list.push({text:'...',value:2,type:'point'});
                    let center = this.currentPage;
                    let lastPage = center+2;
                    if(lastPage < this.pageNum-2){
                        for(let i=center-2;i<=lastPage;i++){
                            list.push({text:i,value:i});
                        }
                        list.push({text:'...',value:this.pageNum-1,type:'point'});
                        list.push({text:this.pageNum,value:this.pageNum});
                    }else{
                        for(let i= this.pageNum-4;i<=this.pageNum;i++){
                            list.push({text:i,value:i});
                        }
                    }
                    return list;
                }
                //当前页数为this.pageNum-4
                if(this.currentPage === this.pageNum-4){
                    list.push({text:1,value:1});
                    list.push({text:'...',value:2,type:'point'});
                    for(let i=this.currentPage-2;i<=this.currentPage+2;i++){
                        list.push({text:i,value:i});
                    }
                    list.push({text:'...',value:this.pageNum-1,type:'point'});
                    list.push({text:this.pageNum,value:this.pageNum});
                    return list;
                }
                //当前页数大于this.page-4
                if(this.currentPage > this.pageNum-4){
                    list.push({text:1,value:1});
                    list.push({text:'...',value:2,type:'point'});
                    for(let i=this.pageNum-4;i<=this.pageNum;i++){
                        list.push({text:i,value:i});
                    }
                    return list;
                }
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
                }else if(!value.type){
                    this.currentPage = value.value||value;
                }

                this.$emit('pageCallback',{currentPage:this.currentPage});
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
            border-radius: 6px;
            &.point{
                border: none;
                cursor: default;
            }
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