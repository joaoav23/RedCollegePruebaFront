<template>
  <div v-if="completed==active || active=='all'"
    class="card w-100 mt-4"
    :class="{
      borderGreen: completed == true,
      borderDanger: completed == false,
    }"
  >
    <NuxtLink :to="'/Todos/' + id" class="text-decoration-none text-dark">
      <div class="card-body">
        <h5 class="card-title">
          <strong class="text-capitalize">{{ title }}</strong>
        </h5>
        <p v-if="completed" class="text-success">Completado</p>
        <p v-else class="text-danger">Incompleto</p>
        <!-- <p class="card-text text-muted">Usuario: {{this.user.name}}</p> -->
      </div>
    </NuxtLink>
  </div>
</template>

<script>
export default {
  name: "TodoComponent",
  props: ["id", "title", "completed", "userId","active"],
};
</script>