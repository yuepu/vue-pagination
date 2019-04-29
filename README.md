## 基于vue封装的分页组件
---
## 组件说明：

1、传参：pageSize（一页多少数据） total（所有的数据）

2、出参：currentPage（点击的当前页）

---
## 使用demo:

1、首先引入pagination

``import Pagination from './components/Pagination/Pagination.vue'; ``

``
export default {
        name: 'app',
        components: {
            Pagination
        },
        data() {
            return {
                pageSize: 2,
                total: 40
            }
        },
        methods:{
            pageCallback:function(data) {
              console.log(data);
            }
        }
    }
``


2、然后使用组件
``
<Pagination :pageSize="pageSize"
                    :total="total"
                    v-on:pageCallback="pageCallback"
        ></Pagination>

``

---
 ## 查看效果地址：[分页组件](https://yuepu.github.io/pagination/)