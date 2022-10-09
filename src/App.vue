<template>
  <v-app>
    <v-main>
      <DruggerTodo />
    </v-main>
  </v-app>
</template>

<script>
import DruggerTodo from "./components/DruggerTodo.vue";

export default {
  name: "App",

  components: {
    DruggerTodo,
  },

  data: () => ({
    //
  }),
};
</script>
