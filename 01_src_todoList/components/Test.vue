<template>
    <div >
        <button @click="isShow = !isShow">显示/隐藏</button>
        <transition appear name="animate__animated animate__bounce" enter-active-class="animate__zoomIn" leave-active-class="animate__zoomOut">
            <div v-show="isShow" class="demo">Todo-List</div>
        </transition>
    </div>
</template>

<script>
    import 'animate.css'
    export default {
        name:"Test",
        data() {
            return {
                isShow:true
            }
        },
    }
</script>

<style scoped>
    .demo{
        width: 560px;
        height: 28px;
        font-size: 20px;
        background-color: rgb(232, 240, 237);
        border: 1px solid #ccc;
        border-radius: 4px;
        padding: 4px 7px;
        text-align: center;
    }

    .anima-enter-active{
        animation: todoTittle 1s;
    }

    .anima-leave-active{
        animation: todoTittle  1s reverse;
    }

    @keyframes todoTittle {
        from{
            transform: translateX(-100%);
        }
        to{
            transform: translateX(0px);
        }
    }
</style>