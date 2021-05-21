<template>
  <div class="container">
    <h1 class="heading mt-5 text-center" style="color : red; font-size:3rem; ">
      My Todo App
    </h1>
    <div class="addTodo">
      <input
        type="text "
        v-model="task"
        placeholder="Enter Your Task Buddy..!!   :) "
        class="form-control text-center"
      />
      <br />
      <div class="text-center">
        <button @click="submit" class="btn btn-warning rounded-0 ">
          Submit
        </button>
      </div>

      <table class="table table-bordered mt-5">
        <thead>
          <tr>
            <th scope="col">Task</th>
            <th scope="col">Status</th>
            <th scope="col" class="text-center">#</th>
            <th scope="col" class="text-center">#</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(todo, index) in todos" :key="index">
            <th>{{ todo.name }}</th>
            <td>{{ todo.status }}</td>
            <td>
              <div class="text-center">
                <span @click="editTask(index)">Edit</span>
              </div>
            </td>
            <td>
              <div class="text-center">
                <span @click="deleteTask(index)">Delete</span>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoApp",
  data() {
    return {
      task: "",
      todos: [
        {
          name: "Going To Toilet",
          status: "Urgent"
        }
      ],
      editedTask: null
    };
  },
  methods: {
    submit() {
      if (this.task.length === 0) return;

      if (this.editedTask === null) {
        this.todos.push({
          name: this.task,
          status: "todo"
        });
      } else {
        this.todos[this.editedTask].name = this.task;
        this.editedTask = null;
      }
    },

    deleteTask(index) {
      this.todos.splice(index, 1);
      console.log("deleteTask");
    },

    editTask(index) {
      this.task = this.todos[index].name;
      this.editedTask = index;
      console.log("editing");
    }
  }
};
</script>


<style scoped>
</style>
