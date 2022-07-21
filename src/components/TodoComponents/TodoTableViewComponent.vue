<template>
  <tbody>
    <tr>
      <th scope="row">{{ index }}</th>
      <td>{{ id }}</td>
      <td>{{ title }}</td>
      <td>{{ description }}</td>
      <td>
        <button class="btn btn-lg" @click="editItemTodo">
          <i class="bi bi-pencil-square text-primary"></i>
        </button>
      </td>
      <td>
        <button class="btn btn-lg" @click="deleteItem">
          <i class="bi bi-trash3-fill text-danger w-100"></i>
        </button>
      </td>
    </tr>
  </tbody>
</template>

<script>
export default {
  name: "TodoTableViewComponent",
  props: {
    index: {
      type: Number,
      required: true,
    },
    id: {
      type: Number,
      required: true,
    },
    title: {
      type: String,
      required: true,
    },
    description: {
      type: String,
      required: true,
    },
    editedId: {
      type: Number,
      required: true,
    },
  },
  emits: ["delteItem", "editItemTodo"],
  methods: {
    editItemTodo() {
      this.$emit("editItemTodo", {
        index: this.index,
        id: this.id,
        title: this.title,
        description: this.description,
      });
    },
    deleteItem() {
      this.$emit("deleteItem", this.index);
    },
  },
};
</script>

<style></style>
