<template>
    <div>
        <h2>{{ title }}</h2>
        <table class="table table-dark">
            <thead> 
                <tr>
                    <th>Id.</th>
                    <th>Nome</th>
                    <th width="150px">Ações</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>1</td>
                    <td>asdfas</td>
                    <td>
                        <a href="">Editar</a>
                        <a href="">Deletar</a>
                        <a href="">Deletar</a>
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
            tasks: []
        } 
    }
}
</script>
<style >

</style>