<template>
  <div class="container vh-100 d-flex align-items-center">
    <!-- <Tutorial/> -->
    <div class="row w-100">
      <h1 class="col-12 text-center">NuxtJs</h1>
      <NuxtLink to="/Todos" class="btn btn-primary btn-lg w-100">Todos</NuxtLink>
      <NuxtLink to="/Tasks" class="btn btn-primary btn-lg w-100 mt-3">Tasks</NuxtLink>
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage'
}
</script>
