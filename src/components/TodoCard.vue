<template>
    <div class="card ">
        <header class="card-header header ">
            <p class="card-header-title">
            {{ today }}
            </p>
            <p class="card-header-title title">
                {{titre}}
            </p>
            <p class="card-header-title">   
             {{count}} tâches en cour
            </p>
        </header>
        <div class="card-content">
            <newTodo class="addTask" @sendTask="addTask"   ></newTodo>
        </div>
       <todoList :tasks="tasks" @checkEvent="checkTask" @delete="removeTask"></todoList>
    </div>
</template>
<script>
import newTodo from "./newTodo";
import todoList from './todo-list'
    export default {
        name: 'todo-card',
        computed: {
            today: function() {
                var d =  new Date();
                var months = ['Janvier', 'Février', 'Mars', 'Avril', 'Mai', 'Juin', 'Juillet', 'Aout', 
                            'Septembre', 'Octobre', 'Novembre', 'Décembre'];
                var days = ['Dimanche', 'Lundi', 'Mardi', 'Mercredi', 'Jeudi', 'Vendredi', 'Samedi'];
                var month = months[d.getMonth()];
                var day = days[d.getDay()];
                var date = d.getDate();
                return day + ' ' + date + ' ' + month;
                } 
            },
            data() {
                return{
                titre : ' VueJS tutorial  TodoList',
                tasks: [],
                count: 0,
                }
            },
            components : { 
                newTodo,
                todoList
            },  
            methods : {
                addTask(name) {
                        let newTask = {
                            checked : false,
                            name: name
                        }
                        this.tasks.push(newTask);
                        this.count += 1;             
                },
                checkTask(index){
                   this.tasks[index].checked =  !this.tasks[index].checked
              
                },
                removeTask(index){
                    this.tasks.splice(index, 1);
                    this.count--;
                }
            }
        }
</script>
<style scoped>
    .card{
        width: 50%;
        border-radius: 5%;
        display: flex;
        flex-direction: column;
    }
    .card-content{
        text-align: center;
    }
    .title{
        color: rgb(7, 206, 7) !important;
    }
</style>