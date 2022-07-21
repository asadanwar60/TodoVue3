<template>
  <div class="container border">
    <h1>Todos</h1>
    <ul>
      <li>
        <input v-model="title" type="text" placeholder="Enter title here " />
      </li>
      <li>
        <input
          v-model="description"
          type="text"
          placeholder="Enter description "
        />
      </li>
      <li>
        <button v-if="index == null" @click="addTodo">Add Todo Item</button>
        <button v-else @click="updateTodo(index, editedId)">
          Update Todo Item
        </button>
      </li>
    </ul>

    <div v-for="(item, index) in todoItem" :key="item.id">
      <ul>
        <li>
          {{ index }} - {{ item.id }} - {{ item.title }} - {{ item.description
          }}<button class="ml-5" @click="deleteTodo(index)">Delete</button>
          <button class="ml-5"
            @click="editTodo(index, item.id, item.title, item.description)"
          >
            Edit
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todoItem: [],
      todoList: null,
      todoEditList: null,
      id: 1,
      title: "",
      description: "",
      editedId: null,
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
    editTodo(index, id, title, description) {
      this.index = index;
      this.editedId = id;
      this.title = title;
      this.description = description;
      console.log(
        this.editedId,
        this.description,
        this.title,
        "Edit Todo fired"
      );
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