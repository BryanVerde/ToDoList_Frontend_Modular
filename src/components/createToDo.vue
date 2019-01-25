<template>
  <div class="container">
    <h1>Create A ToDo</h1>
    <div class="row">
          <div class="col-md-8"></div>
          <div class="col-md-4">
          <router-link :to="{ name: 'home' }" class="btn btn-success">
              Show ToDos</router-link>
          </div>
      </div>
    <form v-on:submit.prevent="addToDo">
      <div class="row">
        <div class="col-md-6">
          <div class="form-group">
            <label>ToDo Title:</label>
            <input type="text" class="form-control" v-model="ToDos.Title">
          </div>
        </div>
        </div>
        <div class="row">
          <div class="col-md-6">
            <div class="form-group">
              <label>ToDo Description:</label>
              <input type="text" class="form-control col-md-6" v-model="ToDos.Description">
            </div>
          </div>
        </div><br />
        <div class="form-group">
          <button class="btn btn-primary">Add ToDo</button>
        </div>
    </form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      ToDos: {},
    };
  },
  methods: {
    addToDo() {
      const uri = 'http://localhost:3000/ToDoList';
      this.axios.post(uri, this.ToDos).then((response) => {
        console.log(response);
        this.ToDos.Title = '';
        this.ToDos.Description = '';
      });
    },
  },
};
</script>
