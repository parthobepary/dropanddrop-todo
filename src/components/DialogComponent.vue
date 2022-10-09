<template>
  <div class="text-center">
    <v-dialog v-model="dialog" width="500">
      <template v-slot:activator="{ on, attrs }">
        <v-btn color="red lighten-2" dark v-bind="attrs" v-on="on">
          Edit item
        </v-btn>
      </template>

      <v-card>
        <v-card-title class="text-h5 grey lighten-2">
          Privacy Policy
        </v-card-title>
        <v-text-field
          v-model="message"
          label="Regular"
          clearable
        ></v-text-field>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" text @click="editItem(index)"> submit </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>
<script>
export default {
  name: "DialogComponent",
  data() {
    return {
      dialog: false,
      message: "",
    };
  },
  props: ["index", "inArray", "id", "time"],
  methods: {
    editItem(id) {
      this.inArray.splice(id, 1);
      var date = new Date();
      var curretnTime = JSON.stringify(date);
      let obItem = {
        name: this.message,
        time: this.time,
        id: this.id,
        you: curretnTime,
      };
      this.inArray.push(obItem);
      console.log(obItem);
      this.dialog = false;
    },
  },
};
</script>

<!-- 
          const id = myObject.getIndex;
      const name = myObject.items;
      console.log(id, name);
      state.myTodo[id] = name;
      state.myTodo = [...state.myTodo];
 -->
