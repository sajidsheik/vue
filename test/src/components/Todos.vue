<template>
    <div>
        <h1>Todos</h1>
         <div v-bind:key="todo.id" v-for="todo in allTodos">          
           <TodoItem v-bind:todo="todo" v-on:del-todo="deleteTodo"/>
         </div>
    </div>
</template>

<script>
import Vue from 'vue';
import { mapGetters, mapActions } from 'vuex';
import TodoItem from './todoitem.vue';
export default Vue.extend({
    name:"Todos",
    props:["todos"],
    computed: mapGetters(['allTodos']),
     created(){
       this.fetchTodos(); 
    }, 
    components:{TodoItem},
    methods : {
        ...mapActions(['fetchTodos','deleteTodo']),
    },
   
})
</script>
<style lang="less" scoped>

</style>