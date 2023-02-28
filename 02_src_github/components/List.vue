<template>
    <div class="row">
        <!-- 用户信息 -->
        <div v-show="info.users.length" class="card" v-for="user in info.users" :key="user.login">
            <a :href="user.html_url" target="_blank">
                <img :src="user.avatar_url" style="width: 100px">
            </a>
            <p class="card-text">{{ user.login }}</p>
        </div>
        <!-- 欢迎界面 -->
        <div v-show="info.isFirst">
            <span>Welcome to Page</span>
        </div>
        <!-- 加载界面 -->
        <div v-show="info.isLoading">
            <span>Loading</span>
        </div>
        <!-- 错误提示 -->
        <div v-show="info.message">
            <span>{{ info.message }}</span>
        </div>
    </div>
</template>

<script>
    export default {
        name:'List',
        data() {
            return {
                info:{
                    isFirst:true,
                    isLoading:false,
                    message:'',
                    users:[]
                }
                
            }
        },
        mounted() {
            this.$bus.$on('updataList',(data)=>{
                this.info = {...this.info,...data}
            })
        },
    }
</script>

<style scoped>
    .album {
        min-height: 50rem; /* Can be removed; just added for demo purposes */
        padding-top: 3rem;
        padding-bottom: 3rem;
        background-color: #f7f7f7;
    }

    .card {
        float: left;
        width: 33.333%;
        padding: .75rem;
        margin-bottom: 2rem;
        border: 1px solid #efefef;
        text-align: center;
    }

    .card > img {
        margin-bottom: .75rem;
        border-radius: 100px;
    }

    .card-text {
        font-size: 85%;
    }
</style>