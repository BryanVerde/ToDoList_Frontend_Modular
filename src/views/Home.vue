<template>
    <div class="container">
        <h1>ToDos</h1>
        <br />
        <div class="row">
            <table class="table table-striped table-hover">
                <thead>
                    <tr>
                        <!--<th>ID</th>-->
                        <th>Title</th>
                        <th>Description</th>
                        <th></th>
                        <th></th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="ToDo in ToDos" :key="ToDo._id">
                        <!--<td>{{ ToDo._id }}</td>-->
                        <td>{{ ToDo.Title }}</td>
                        <td>{{ ToDo.Description }}</td>
                        <td><router-link :to="{ name: 'updateToDo', params: { id: ToDo._id } }" class="btn btn-warning">
                Update</router-link>&nbsp&nbsp&nbsp&nbsp&nbsp<button class="btn btn-danger" v-on:click="deleteToDo(ToDo._id, index)">Delete</button></td>
                    </tr>
                </tbody>
            </table>
        </div>
        <div class="row">
            <div class="col-md-8"></div>
            <div class="col-md-4">
            <router-link :to="{ name: 'createToDo' }" class="btn btn-primary">
                Create ToDo</router-link>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return{
            ToDos: []
        }
    },
    created: function()
    {
        this.fetchToDo();
    },
    methods: {
        fetchToDo()
        {
            const uri = 'http://192.168.99.100:3000/ToDoList';
            this.axios.get(uri).then((response) => {
                this.ToDos = response.data;
            });
        },
        deleteToDo(id, index)
        {
            const uri = 'http://192.168.99.100:3000/ToDoList/' + id;
            this.axios.delete(uri, this.ToDos)
                .then(response => {
                    this.fetchToDo();
                })
            /*this.axios.delete(uri, this.ToDos)
                .then(response => this.ToDos.splice(index, 1))
                .then(response => this.fetchToDo())
                .catch(err => console.error(err))*/
        },
    },
};
</script>
