<template>
    <div class="article-view">
        <Header type="2">
            <span class="title" slot="title">懂球帝</span>
            <span slot="right"></span>
        </Header>
        <div class="content cal-wrapper">
            <div class="wrap">
                <div v-html="articleText"></div>
            </div>
        </div>
    </div>
</template>

<script>
    import BScroll from 'better-scroll'
    import {calHeight} from '../../assets/js/utils'
    import {reqArtHTML} from '../../api'
    import Header from '../../components/Header/Header'

    export default {
        data() {
            return {
                description:'', // 文章描述对象
                articleText:'',
            }
        },
        async created(){
            this.articleText = await reqArtHTML(this.$route.params.id)
        },
        mounted(){
            this.$nextTick(() => {
                calHeight(1.95)
                new BScroll('.content',{
                    scrollY:true,
                    click:true,
                })
            })
        },
        components:{Header}
    }
</script>

<style lang="stylus" rel="stylesheet/stylus">
    .article-view
        padding-top 1.95rem
</style>