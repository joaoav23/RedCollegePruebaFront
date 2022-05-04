<template>
  <div class="container pt-4">
        <h1 class="mt-4">
          <strong class="text-capitalize"
            >Todo n°{{ todo.id }} {{ todo.title }}</strong
          >
        </h1>
        
        <div class="targeta">
          <h2><strong>Usuario</strong></h2>
          <hr />
          <h4><strong>Nombre: </strong>{{user.name}}</h4>
          <h4><strong>Nombre de usuario: </strong>{{user.username}}</h4>
          <h4><strong>Email: </strong>{{user.email}}</h4>
        </div>

        <NuxtLink to="/Todos" class="btn btn-primary btn-lg mt-4" >Volver</NuxtLink>
    </div>
</template>

<script>
export default {
  async asyncData({ $axios, params }) {
    const todo = await $axios.get(
      "https://jsonplaceholder.typicode.com/todos/" + params.id
    );

    const user = await $axios.get(
      "https://jsonplaceholder.typicode.com/users/" + todo.data.userId
    );

    return {
      user: user.data,
      todo: todo.data,
    };
  },
  created() {
    console.log(this.user);
    // console.log(this.$route.params.id);
  },
};
</script>

<style>
.targeta {
  padding: 30px;
  box-shadow: 0px 0px 5px black;
  border-radius: 10px;
  margin-top: 40px;
}
</style>