<template>
    <ul>
        <li v-for="item in imgList">
            <img :src="item.img_url" :alt="item.title">
            <span>{{item.title}}</span>
        </li>
        <!--<li v-if="newsList.length < 1">
            <span>暂无新闻</span>
        </li>-->
        <li>
            <button @click="btnClick('pre')">上一页</button>
            <button @click="btnClick('next')">下一页</button>
        </li>
    </ul>
</template>

<script>
    export default {
        name: 'MeiZi',
        data(){
            return {
                imgList: [],
                currentPage: 0
            }
        },
        mounted(){
            this.getImgs();
        },
        methods: {
            btnClick(num){
                if(num==='pre' && this.currentPage < 2){ alert('已经是第一页了'); return}
                this.getImgs(num);
            },
            getImgs(num){

                let pageNum = num==='pre'? this.currentPage-1 : this.currentPage+1;
                console.log('下一页');
                this.$http.get(`http://192.168.1.78:3000/getList/${pageNum}`)
                    .then(({data}) => {
                        this.imgList = [...data];
                        num==='pre'? this.currentPage--: this.currentPage++;
                    }).catch(e => {
                        alert('获取数据失败。');
                });

            }
        }
    }
</script>

<style scoped>

    ul {
        list-style: none;
    }

    li {
        text-align: center;
        margin: 20px 0;
    }

    img {
        width: 236px;
        height: 354px;
        display: block;
        margin: 0 auto;
    }
</style>
