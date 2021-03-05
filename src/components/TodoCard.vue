<template>
    <div class="card ">
        <header class="card-header header ">
            <p class="card-header-title">
            {{ today }}
            </p>
            <p class="card-header-title title">
                {{titre}}
            </p>
            <p class="card-header-title" v-if="tasks.length > 1">   
             {{tasks.length}} tâches en cour
            </p>
           <p class="card-header-title" v-else>   
             {{tasks.length}} tâche en cour
            </p>
           
        </header>
        <div class="card-content">
            <div >
                 <newTodo class="addTask" @sendTask="addTask"></newTodo>
            </div>
            <div>
                   <button v-if="tasks.length > 1"  @click="removeAllTask" class="button is-danger mt-3">Supprimer toutes les tâches</button>
            </div>
             <div>
                   <button v-if="tasks.length > 1"  @click="removeAllTaskChecked" class="button is-warning mt-3"  >Supprimer toutes les tâches terminé</button>
            </div>
         
            
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
                tasks: [],
                titre : ' VueJS tutorial  TodoList',
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
                },
                checkTask(index){
                   this.tasks[index].checked =  !this.tasks[index].checked
              
                },
                removeTask(index){
                    // remove task if check
                    // if( this.tasks[index].checked){
                    //     this.tasks.splice(index, 1);
                    // }
                    this.tasks.splice(index, 1);
                },
                removeAllTask(){
                    this.tasks.splice(0);
                },
                removeAllTaskChecked(){
                    for(let index = 0 ; index < this.tasks.length ; index++){
                        if(this.tasks[index].checked){
                            this.tasks.splice(index, 1);
                        }
                    }   
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
        flex-flow: column wrap;
    }
    .title{
        color: rgb(7, 206, 7) !important;
    }
</style>