<template>
  <div class="container my-4">
    

    <div class="row justify-content-center">
      
      <div class="card p-3 mt-4 col-6">
        <h1 v-if="id == null">Nueva Tarea</h1>
    <h1 v-if="id != null">Editar Tarea</h1>
        <form @submit.prevent="actionTask">
          <div class="row px-0 mx-0">
            <label class="col-12 px-0">Nombre:</label>
            <input
              type="text"
              class="from-control col-12"
              name="name"
              v-model="task.name"
            />
      
            <label class="col-12 px-0">Descripcion:</label>
            <input
              type="text"
              class="from-control col-12"
              name="description"
              v-model="task.description"
            />
      
            <label class="col-12 px-0">Estado:</label>
            <select
              name="status"
              class="form-control col-12"
              v-model="task.status"
            >
              <option value="1">Completado</option>
              <option value="2">Pendiente</option>
            </select>
          </div>
      
          <input
            type="submit"
            value="Guardar"
            class="btn btn-primary mt-4 w-100"
          />
          <NuxtLink class="btn btn-warning mt-4 w-100" to="/Tasks">Volver</NuxtLink>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["id", "task"],
  methods: {
    actionTask() {
      if (this.id != null) {
        this.updateTask();
      } else {
        this.saveTask();
      }
    },
    async updateTask() {
      if (this.validateForm()) {
        alert("rellena todos los campos");
      } else {
        const task = await this.$axios.post(
          "http://127.0.0.1:3333/api/v1/task/update/" + this.id,
          this.task
        );

        await alert(
          "La tarea: " +
            task.data.name +
            " ha sido actualizada con exito has click en aceptar para volver"
        );
        this.$router.push("/Tasks/");
      }
    },
    async saveTask() {
      if (this.validateForm()) {
        alert("rellena todos los campos");
      } else {
        const newTask = await this.$axios.post(
          "http://127.0.0.1:3333/api/v1/task/save",
          this.task
        );

        await alert(
          "La tarea: " +
            newTask.data.name +
            "ha sido creada con exito has click en aceptar para volver"
        );
        this.$router.push("/Tasks/");
      }
    },
    validateForm() {
      if (
        this.task.name == "" ||
        this.task.description == "" ||
        this.task.status == ""
      ) {
        return true;
      }
    },
  },
};
</script>