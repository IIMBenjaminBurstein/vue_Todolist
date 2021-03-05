<template>
        <input v-model.trim="task" class="input is-primary" type="text" placeholder="Nouvelle Tâche">
        <i v-on:click="newTask" class="fas fa-plus-circle plus"></i>
</template>
<script>
export default {
    name: 'new-todo',
    data() {
        return{
        task: '',
        }
    },
    methods: {
        newTask() {
            if(this.task != ''){
                this.$emit("sendTask", this.task)
            }
            
        }
    }
}
</script>
<style scoped>
    input{
        width: 60%;
        border: none;
        border-bottom:  solid green 2px;
      
    }
    .plus{
        color: green;
        font-size: 40px;
        margin-left : 2%
    }   
</style>