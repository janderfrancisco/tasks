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
            <form action="form form-inline">
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
                        <a href="#" @click.prevent="editTask(task.id)" class="btn btn-info">Editar</a>
                        <a href="#"@click.prevent="deleteTask(task.id)"  class="btn btn-danger">Deletar</a>
                      
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
        editTask (id){
            this.updateIndex = this.findIndexItem(id)
            this.updating = true
            this.task = this.tasks[this.updateIndex]
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
        deleteTask (id){
            let index = this.findIndexItem(id)
            this.tasks.splice(index, 1)
        },
        findIndexItem(id){
            for (let index = 0; index < this.tasks.length - 1; index++) {
                if(this.tasks[index].id === id)
                    return index               
            }
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