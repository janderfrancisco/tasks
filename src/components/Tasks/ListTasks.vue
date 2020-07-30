<template>
    <div>
        <h2>{{ title }}</h2>
        <div class="row">

        <div class="col">
            <form action="form form-inline" @submit.prevent="onSubmit()">
                <input type="text" name="" placeholder="Nome da tarafa" class="form-control" v-model="task.name">
                <button type="submit" class="btn btn-primary">Enviar</button>
            </form>
        </div>
        <div class="col">
            <form action="form form-inline" @submit.prevent="onSubmit()">
                <input type="text" name="" placeholder="Nome da tarafa" class="form-control" v-model="filter">
               
            </form>

            </div>
        </div>
        <table class="table table-dark">
            <thead> 
                <tr>
                    <th>Id.</th>
                    <th>Nome</th>
                    <th width="150px">Ações</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(task, index) in filteredTask"  :key="index">
                    <td>{{ task.id }}</td>
                    <td>{{ task.name }}</td>
                    <td>
                        <a href="#" @click.prevent="editTask(index)" class="btn btn-info">Editar</a>
                        <a href="#"@click.prevent="deleteTask(index)"  class="btn btn-danger">Deletar</a>
                      
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    data(){
        return{
            title: 'Lista de Tarefas',
            tasks: [],
            task:{
                id: '',
                name: ''
            },
            updating: false,
            updateIndex: '',
            filter: ''
        } 
    },
    methods:{
        onSubmit (){
            if ( this.updating){
                this.update()
                return;
            }

            this.saveTask()
        },
        saveTask(){
            let idTask = this.tasks.length + 1
            this.task.id = idTask

            this.tasks.push(this.task)
            this.clearForm() 
        },
        editTask (index){
            this.updating = true
            this.updateIndex = index
            this.task = this.tasks[index]
        },
        update(){
            this.tasks[this.updateIndex] = this.task
            this.updating = false
            this.clearForm()
        },
        clearForm(){
            this.task =  {
                id: '',
                name: ''
            } 
        },
        deleteTask (index){
            this.tasks.splice(index, 1)
        }
    },
    computed:{
        filteredTask (){
            if (this.filter === '')
                return this.tasks
            
            let vm = this
            return this.tasks.filter(task => {
                return task.name.toLowerCase().indexOf(vm.filter.toLowerCase()) > -1
            })
            
        }
    }
}
</script>
<style scoped>
form{
    margin: 20px 0
}

 
</style>