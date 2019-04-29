<template>
    <div id="app">
        <Pagination :pageSize="pageSize"
                    :total="total"
                    v-on:pageCallback="pageCallback"
        ></Pagination>
    </div>
</template>
<script>
    import Pagination from './components/Pagination/Pagination.vue';

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
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
