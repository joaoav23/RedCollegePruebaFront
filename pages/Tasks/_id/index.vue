<template>
    <FormComponent
      :id="id"
      :task="task"
    />
</template>

<script>
export default {
  head() {
    return {
      title: "Editar tarea",
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
  async asyncData({ $axios, params }) {
    const task = await $axios.post("http://127.0.0.1:3333/api/v1/task/"+params.id);
    return {
      task: {
        name: task.data.name,
        description: task.data.description,
        status:task.data.status,
      },
      id:task.data.id,
    };
  }
};
</script>