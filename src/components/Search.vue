<template>
    <section class="jumbotron">
        <h3 class="jumbotron-heading">Search Github Users</h3>
        <div>
            <input type="text" placeholder="enter the name you search" v-model="keyWords"/>&nbsp;
            <button @click="getUsers">Search</button>
        </div>
    </section>
</template>

<script>
    import axios from 'axios';
    export default {
        name:'Search',
        data() {
            return {
                keyWords:[]
            }
        },
        methods: {
            getUsers(){
                this.$bus.$emit('updataList',{
                    isFirst:false,
                    isLoading:true,
                    message:'',
                })
                axios.get('https://api.github.com/search/users?q='+this.keyWords).then(
                    response => {
                        console.log('请求成功')
                        this.$bus.$emit('updataList',{
                            isLoading:false,
                            message:'',
                            users:response.data.items
                        })

                    },
                    error => {
                        console.log('请求失败')
                        this.$bus.$emit('updataList',{
                            isLoading:false,
                            message:error.message,
                            users:[]
                        })
                    } 
                )
            }
        },
    }
</script>

<style>

</style>