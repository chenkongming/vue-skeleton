<template>
    <div class="home-wrapper">
        <!--仅仅移除骨架屏组件即可-->
        <vueSkeleton v-if="loading"></vueSkeleton>
        <div class="banner skeleton-square">
            <img :src="banner" alt="">
        </div>
        <div class="logo-wrapper">
            <div class="logo skeleton-circular" v-for="a in 3" :key="'logo'+a"></div>
        </div>
        <div class="content"></div>
    </div>
</template>

<script type="text/ecmascript-6">
import vueSkeleton  from './index'
    export default {
       name:'vueSkeleton',
        components:{vueSkeleton},
        data(){
           return{
               loading:true,
               // 如有需要，先默认数据以撑开元素大小和位置
               banner:'http://img5.imgtn.bdimg.com/it/u=1768436016,3486987531&fm=26&gp=0.jpg',
           }
        },
        created() {
           this.getData()
        },
        methods:{
            getData(){
                setTimeout(()=>{
                    this.loading=false
                },300)
            }
        }
    }
</script>

<style lang="scss" scoped>
@import "./index";
.home-wrapper{
    width: 100%;
    .banner{
        width: 100%;
        height: 175px;
    }
    .logo-wrapper{
        width: 100%;
        padding: 0 15px;
        box-sizing: border-box;
        display: flex;
        .logo{
            border-radius: 50%;
            width: 105px;
            height: 105px;
            margin-right: 15px;
            &:last-child{
                margin-right: 0;
            }
        }
    }
    .content{
        width: 100%;
        height: 300px;
    }
}
</style>
