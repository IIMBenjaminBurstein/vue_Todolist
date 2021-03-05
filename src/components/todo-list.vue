<template>
<div class="todolist"  v-for="(task, index) in tasks" :key="(task, index)">
    <div class="round">
        <input @click="check(index)" class="checkbox" type="checkbox"  />
    </div>
    <p v-bind:class="{'checked' : task.checked }">{{task.name}}</p>
    <i class="far fa-trash-alt poubelle" @click="remover(index)"></i>
</div>
    

</template>
<script>
export default {
    name: 'TodoList',
    props: ['tasks'],   
    methods: {
      check(index){
       this.$emit('checkEvent', index);
     
      },
      remover(index){
        this.$emit('delete', index)
      }
        }
    }

    </script>
    <style scoped>
    .poubelle{
    color: red;
    font-size: 40px;
}
.todolist{
    display: flex;
    justify-content: space-between;
    max-width: 70%;

    margin: 0 0 20px 12%;
}

.checked{
    color: red;
}
</style>