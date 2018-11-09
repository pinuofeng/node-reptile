<template>
    <ul>
        <li v-for="item in newsList">
            <a :href="item.news_url" target="_blank">{{item.title}}</a>
            <span>{{item.time}}</span>
        </li>
        <li v-if="newsList.length < 1">
            <span>暂无新闻</span>
        </li>
        <li>
            <button @click="btnClick('pre')">上一页</button>
            <button @click="btnClick('next')">下一页</button>
        </li>
    </ul>
</template>

<script>
    export default {
        name: 'HelloWorld',
        data(){
            return {
                newsList: [],
                currentPage: 0
            }
        },
        mounted(){
            this.getNews();
        },
        methods: {
            btnClick(num){
                if(num==='pre' && this.currentPage < 2){ alert('已经是第一页了'); return}
                this.getNews(num);
            },
            getNews(num){
                let pageNum = num==='pre'? this.currentPage-1 : this.currentPage+1;
                this.$http.get(`http://192.168.1.78:3000/getList/${pageNum}`)
                    .then(({data}) => {
                        this.newsList = [...data];
                        num==='pre'? this.currentPage--: this.currentPage++;
                    }).catch(e => {
                        alert('获取数据失败。');
                });

            }
        }
    }
</script>

<style scoped>

    div {

    }

    ul {
        list-style: none;
    }

    li {
        text-align: center;
        margin: 20px 0;
    }

    a {
        margin-right: 20px;
        color: #42b983;
    }
</style>
