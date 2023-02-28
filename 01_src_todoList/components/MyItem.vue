<template>
    <transition appear name="animate__animated animate__bounce" enter-active-class="animate__slideInRight" leave-active-class="animate__slideOutRight">
        <li>
            <div>
                <label>
                    <input type="checkbox" :checked="todo.done" @change="checkType(todo.id)"/>
                    <span v-show="!todo.isEdit">{{ todo.thing }}</span>
                    <input type="text" v-show="todo.isEdit" :value="todo.thing" @blur="checkBlur(todo,$event)" ref="inputFocus">
                </label>
                <button class="btn btn-danger" @click="deleteType(todo.id)">删除</button>
                <button class="btn btn-edit" v-show="!todo.isEdit" @click="editType(todo)">编辑</button>
            </div>
        </li>
    </transition>
</template>

<script>
    import 'animate.css'
    export default {
        name:"MyItem",
        props:['todo'],
        methods: {
            checkType(id){
                this.$bus.$emit('checkId',id)
            },
            deleteType(id){
                if(confirm("确定删除吗？"))
                    this.$bus.$emit('deleteTodo',id)
            },
            editType(todo){
                if(todo.hasOwnProperty('isEdit')){
                    todo.isEdit = true
                }else{
                    this.$set(todo,'isEdit',true)
                }
                this.$nextTick(function(){
                    this.$refs.inputFocus.focus()
                })
            },
            checkBlur(todo,e){
                todo.isEdit = false
                this.$bus.$emit('updataTodo',todo.id,e.target.value)
            }
        },
        mounted() {
            
        },
    }
</script>

<style scoped>
    /*item*/
    li {
        list-style: none;
        height: 36px;
        line-height: 36px;
        padding: 0 5px;
        border-bottom: 1px solid #ddd;
    }
    li label {
        float: left;
        cursor: pointer;
    }
    li label li input {
        vertical-align: middle;
        margin-right: 6px;
        position: relative;
        top: -1px;
    }
    li button {
        float: right;
        display: none;
        margin-top: 3px;
    }
    li:before {
        content: initial;
    }
    li:last-child {
        border-bottom: none;
    }
    li:hover{
        background-color:#ddd;
    }
    li:hover button{
        display: block;
    }
</style>