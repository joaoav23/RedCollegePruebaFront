<template>
  <div class="container">
    <h1 class="mt-4"><strong>Todolist</strong></h1>

    <div class="d-flex justify-content-between">

      <div>
        <button
          class="btn1"
          :class="{ active: active == 'all' }"
          @click="buscar('all')"
        >
          Todos
        </button>
        <button
          class="btn1"
          :class="{ active: active == true }"
          @click="buscar(true)"
        >
          Completos
        </button>
        <button
          class="btn1"
          :class="{ active: active == false }"
          @click="buscar(false)"
        >
          Incompletos
        </button>
      </div>
      
      <NuxtLink class="btn btn-warning" to="/">Volver al menu principal</NuxtLink>

    </div>

    <Todo
      v-for="todo in todos"
      :key="todo.id"
      :id="todo.id"
      :title="todo.title"
      :completed="todo.completed"
      :userId="todo.userId"
      :active="active"
    />
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: "Todolist",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Website jsholder",
        },
      ],
      htmlAttrs: {
        lang: "es",
      },
    };
  },
  async asyncData({ $axios }) {
    const todos = await $axios.get(
      "todos"
    );

    return {
      todos: todos.data,
    };
  },
  mounted() {
    // console.log(this.users);
  },
  data() {
    return {
      active: "all",
    };
  },
  methods: {
    buscar(filter) {
      this.active = filter;
    },
  },
};
</script>

<style scoped>
.borderGreen {
  border-left: 6px solid green;
  border-radius: 10px;
}

.borderDanger {
  border-left: 6px solid red;
  border-radius: 10px;
}

.card {
  transition: 150ms ease-in;
}
.card:hover {
  transform: scale(1.02, 1.02);
}

.btn1 {
  border-radius: 12px;
  background-color: transparent;
  box-shadow: none;
  border: none;
  padding: 8px;
}
.active,
.btn1:hover {
  background-color: rgb(0, 87, 201);
  border-radius: 12px;
  color: white;
}
</style>