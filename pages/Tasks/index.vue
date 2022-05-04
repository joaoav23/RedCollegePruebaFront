<template>
  <div class="container my-4">
    <h1>Tareas</h1>
    <div class="row justify-content-between px-3">
      <NuxtLink class="btn btn-success mt-4" to="/Tasks/new"
        >NUEVA TAREA</NuxtLink
      >
      <NuxtLink class="btn btn-warning mt-4" to="/">Volver al menu principal</NuxtLink>
    </div>

    <div class="mt-4 card">
      <table class="table">
        <thead>
          <tr>
            <th scope="col">ID</th>
            <th scope="col">Nombre</th>
            <th scope="col">Descripcion</th>
            <th scope="col">Estado</th>
            <th scope="col">Acciones</th>
          </tr>
        </thead>

        <tbody>
          <div v-if="tasks && tasks.length === 0" class="text-center p-3 col-12 w-100">
            Lista de tareas vacia
          </div>
          <tr v-for="task in tasks" :key="task.id">
            <th scope="row">{{ task.id }}</th>
            <td>{{ task.name }}</td>
            <td>{{ task.description }}</td>
            <td>
              <span
                class="badge"
                :class="{
                  'bg-success': task.status == 1,
                  'bg-warning': task.status == 2,
                }"
              >
                <div v-if="task.status == 1">Completada</div>
                <div v-else>Pendiente</div>
              </span>
            </td>
            <td>
              <NuxtLink class="btn btn-warning btn-sm" :to="'/Tasks/' + task.id"
                >Editar</NuxtLink
              >
              <button
                class="btn btn-danger btn-sm"
                @click="deleteTask(task.id)"
              >
                Eliminar
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: "Tareas",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Website Task api",
        },
      ],
      htmlAttrs: {
        lang: "es",
      },
    };
  },
  async asyncData({ $axios }) {
    const tasks = await $axios.get("http://127.0.0.1:3333/api/v1/task");
    return {
      tasks: tasks.data,
    };
  },
  methods: {
    async deleteTask(id) {
      var opcion = confirm("Estas seguro que deseas eliminar esta tarea?");
      if (opcion) {
        const taskDelete = await this.$axios.delete(
          "http://127.0.0.1:3333/api/v1/task/" + id
        );
        const taskPosition = (task) => task.id == id;
        const position = this.tasks.findIndex(taskPosition);

        this.tasks.splice(position, 1);
        console.log(this.tasks);
      }

      // console.log(taskDelete);
    },
  },
};
</script>