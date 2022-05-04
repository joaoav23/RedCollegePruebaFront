<template>
  <FormComponent :id="null" :task="task" />
</template>

<script>
export default {
  head() {
    return {
      title: "Nueva Tarea",
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
  data() {
    return {
      task: {
        name: "",
        description: "",
        status: "",
      },
    };
  },
};
</script>
