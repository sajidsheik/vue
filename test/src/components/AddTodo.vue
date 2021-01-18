<template>
  <div>
      <form @submit="onSubmit">
          <input type="text" v-model="title" name="title" placeholder="Add Todo">
          <input type="submit" value="submit" class="btn">
       </form>
  </div>  
</template>

<script lang="ts">
import Vue from 'vue';
import {mapActions } from 'vuex'

export default Vue.extend({
    name:"AddTodo",
    data() {
        return {
            title:''
        }
    },
    methods:{
        ...mapActions(['addTodo']),
        onSubmit(e){
            e.preventDefault();
            this.addTodo(this.title);
        }

    }
})
</script> 

<style scoped>
form{
    display: flex;
}

input[type="text"]{
    flex:10;
    padding:5px;
}

input[type="submit"]{
    flex:2;
}
</style>