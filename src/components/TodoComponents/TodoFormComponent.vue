<template>
  <div class="container mt-5">
    <div class="row">
      <div class="col-lg-4 d-none d-lg-block"></div>
      <div class="col-lg-4 col-sm-12 text-center border p-5">
        <h2>Todo App</h2>
        <input
          v-model="title"
          edited
          type="text"
          class="form-control w-100 mt-3 mb-3"
          placeholder="Enter Title Here"
        />
        <input
          v-model="description"
          type="text"
          edited
          class="form-control w-100 mt-3 mb-3"
          placeholder="Enter Description Here"
        />
        <button
          v-if="index == null"
          @click="addTodo"
          class="btn btn-primary w-100"
        >
          Add Todo
        </button>
        <button
          v-else
          @click="updateTodo(index, editedId)"
          class="btn btn-primary w-100"
        >
          Update Todo
        </button>
      </div>
      <div class="col-lg-4 d-none d-lg-block"></div>
    </div>
  </div>

  <div class="container mt-5">
    <hr />
    <h2>Todo List</h2>
    <table class="table table-striped border">
      <thead class="bg-primary text-light">
        <tr>
          <th scope="col">INDEX</th>
          <th scope="col">ID</th>
          <th scope="col">TITLE</th>
          <th scope="col">DESCRIPTION</th>
          <th scope="col">EDIT</th>
          <th scope="col">DELETE</th>
        </tr>
      </thead>
      <TodoTableViewComponent
        v-for="(item, index) in todoItem"
        :index="index"
        v-bind="item"
        :key="item.id"
        @deleteItem="deleteTodo(index)"
        @editItemTodo="editTodo"
      ></TodoTableViewComponent>
    </table>
  </div>
</template>

<script>
import TodoTableViewComponent from "./TodoTableViewComponent.vue";

export default {
  components: { TodoTableViewComponent },
  name: "TodoFormComponent",
  data() {
    return {
      todoItem: [
        { id: 1, title: "Apple", description: "This is fruit" },
        { id: 2, title: "Spinach", description: "This is vegetable" },
      ],
      //   todoList: null,
      //   todoEditList: null,
      id: 3,
      title: "",
      description: "",
      editedId: null,
      index: null,
    };
  },
  methods: {
    addTodo() {
      console.log("add todo fired");
      this.todoList = {
        id: this.id++,
        title: this.title,
        description: this.description,
      };
      this.todoItem.push(this.todoList);
      (this.title = ""), (this.description = "");
    },
    deleteTodo(index) {
      console.log("Delete Todo fired");
      this.todoItem.splice(index, 1);
    },
    editTodo(obj) {
      // console.log(obj)
      this.index = obj.index;
      this.editedId = obj.id;
      this.title = obj.title;
      this.description = obj.description;
      console.log(this.index, this.editedId, this.title, this.description);
    },
    updateTodo(index, id) {
      console.log(index, id);
      this.editedId = id;
      this.todoEditList = {
        id: this.editedId,
        title: this.title,
        description: this.description,
      };
      this.todoItem.splice(index, 1, this.todoEditList);
      console.log(this.editedId, this.todoEditList, "Update Todo fired");
      this.title = "";
      this.description = "";
      this.index = null;
    },
  },
};
</script>

<style></style>
