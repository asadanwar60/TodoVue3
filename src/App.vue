<template>
  <!--navbar-->

  <nav
    class="navbar navbar-expand-lg navbar-dark bg-primary bg-gradient text-light"
  >
    <div class="container-fluid">
      <a class="navbar-brand" href="#">Navbar</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#">Home</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Link</a>
          </li>
          <li class="nav-item dropdown">
            <a
              class="nav-link dropdown-toggle"
              href="#"
              id="navbarDropdown"
              role="button"
              data-bs-toggle="dropdown"
              aria-expanded="false"
            >
              Dropdown
            </a>
            <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
              <li><a class="dropdown-item" href="#">Action</a></li>
              <li><a class="dropdown-item" href="#">Another action</a></li>
              <li><hr class="dropdown-divider" /></li>
              <li><a class="dropdown-item" href="#">Something else here</a></li>
            </ul>
          </li>
          <li class="nav-item">
            <a class="nav-link disabled">Disabled</a>
          </li>
        </ul>
        <form class="d-flex" role="search">
          <input
            class="form-control me-2"
            type="search"
            placeholder="Search"
            aria-label="Search"
          />
          <button class="btn btn-outline-success" type="submit">Search</button>
        </form>
      </div>
    </div>
  </nav>

  <!--Todo form -->
  <div class="container mt-5">
    <div class="row">
      <div class="col-lg-4 d-none d-lg-block"></div>
      <div class="col-lg-4 col-sm-12 text-center border p-5">
        <h2>Todo App</h2>
        <input
          v-model="title"
          type="text"
          class="form-control w-100 mt-3 mb-3"
          placeholder="Enter Title Here"
        />
        <input
          v-model="description"
          type="text"
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

  <!--Todo Table view-->
  <div class="container mt-5">
    <hr>
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
      <tbody v-for="(item, index) in todoItem" :key="item.id">
        <tr>
          <th scope="row">{{ index }}</th>
          <td>{{ item.id }}</td>
          <td>{{ item.title }}</td>
          <td>{{ item.description }}</td>
          <td>
            <button
              class="btn btn-lg"
              @click="editTodo(index, item.id, item.title, item.description)"
            >
              <i class="bi bi-pencil-square text-primary"></i>
            </button>
          </td>
          <td>
            <button class="btn btn-lg" @click="deleteTodo(index)">
              <i class="bi bi-trash3-fill text-danger w-100"></i>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todoItem: [
        { id: 1, title: "Apple", description: "This is fruit" },
        { id: 2, title: "Spinach", description: "This is vegetable" },
      ],
      todoList: null,
      todoEditList: null,
      id: 3,
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
