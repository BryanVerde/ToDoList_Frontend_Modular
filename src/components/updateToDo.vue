<template>
    <div class="container">
        <h1>Update ToDo</h1>
        <div class="row">
          <div class="col-md-10"></div>
          <div class="col-md-2"><router-link :to="{ name: 'home' }" class="btn btn-success">Return to ToDos</router-link></div>
        </div>
        <form v-on:submit.prevent="updateToDos">
            <div class="form-group">
                <label>ToDo Title</label>
                <input type="text" class="form-control" v-model="ToDos.Title">
            </div>
            <div class="form-group">
                <label name="product_Details">ToDo Details</label>
                <input type="text" class="form-control" v-model="ToDos.Description">
            </div>
            <div class="form-group">
                <button class="btn btn-primary">Update</button>
            </div>
        </form>
    </div>
</template>
<script>
export default {
    data() {
        return{
            ToDos: {}
        }
    },
    created: function() {
        this.getToDos()
    },
    methods: {
        getToDos()
        {
            const uri = 'http://localhost:3000/ToDoList/' + this.$route.params.id;
            this.axios.get(uri).then((response) => {
                this.ToDos = response.data;
                console.log(this.ToDos)
            })
        },
        updateToDos()
        {
            const uri = 'http://localhost:3000/ToDoList/' + this.$route.params.id;
            this.axios.put(uri, this.ToDos).then((response) => {
                this.$router.push({ name: 'home' })
            })
        },
    },
}
</script>