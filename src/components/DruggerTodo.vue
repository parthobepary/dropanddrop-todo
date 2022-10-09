<!-- <template>
  <div>
    <div>
      <h1>Add new itam</h1>
      <hr />
      <div>
        <input v-model="inputtext" class="inputBox" type="text" name="" id="" />
        <button @click="addItem">Add</button>
      </div>
    </div>
    <div class="container">
      <div class="Uncompleted">
        <h3>Uncompleted</h3>
        <hr />
        <draggable
          class="list-group"
          :list="list1"
          :clone="clone"
          :group="{ name: 'people', pull: pullFunction }"
          @start="start"
          @change="log"
        >
          <div class="list-item" v-for="(element, index) in list1" :key="index">
            <p :class="{ active: element.status }">{{ element.name }}</p>
          </div>
        </draggable>
      </div>

      <div class="Completed">
        <h3>Completed</h3>
        <hr />
        <draggable
          class="list-group"
          :list="list2"
          :clone="clone"
          :group="{ name: 'people', pull: pullFunction }"
          @change="log"
        >
          <div
            class="list-item"
            @start="start(index)"
            v-for="(element, index) in list2"
            :key="index"
          >
            <p :class="{ active: element.status }">{{ element.name }}</p>
          </div>
        </draggable>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";
export default {
  name: "DruggerTodo",
  components: {
    draggable,
  },
  data() {
    return {
      inputtext: "",
      list1: [
        { name: "Luc", status:  "12-49-20"" },
        { name: "Thomas", status: "null" },
        { name: "John", status: "null" },
      ],
      list2: [{ name: "Jesus", status: null }],
      controlOnStart: true,
    };
  },
  methods: {
    clone({ name }) {
      return { name, status };
    },
    pullFunction() {
      return this.controlOnStart ? "clone" : true;
    },
    start({ originalEvent }) {
      this.controlOnStart = originalEvent.ctrlKey;
    },
    log: function (evt) {
      if (evt.added) {
        if (evt.added.element.status === "null") {
          evt.added.element.status = null;
        } else if (evt.added.element.status === null) {
          evt.added.element.status = "null";
        }
      }
    },
    addItem() {
      this.list1.push({ name: this.inputtext, status: "null" });
      this.inputtext = "";
    },
  },
};
</script>
<style scoped>
.active {
  text-decoration: line-through;
}
.inputBox {
  width: 250px;
  height: 30px;
  border: none;
  border-bottom: 2px solid red;
  outline: none;
}
button {
  width: 100px;
  height: 30px;
  margin-left: 5px;
}
.container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  padding: 10px 50px;
}
.Uncompleted {
  background-color: cadetblue;
  padding: 10px;
  border-radius: 10px;
}
.Completed {
  background-color: rgb(124, 160, 95);
  padding: 10px;
  border-radius: 10px;
}
.list-item {
  background-color: azure;
  border-radius: 10px;
  margin-bottom: 5px;
  width: 200px;
  padding: 10px;
}
</style>
 -->

<template>
  <div class="container">
    <div class="box">
      <div class="flex">
        <h3>Todo</h3>
        <button @click="isClick = !isClick">+</button>
      </div>
      <div v-if="isClick" class="addedbox">
        <input v-model="todoinput" type="text" />
        <br />
        <button @click="addToTodo(todoinput)">Add</button>
        <button @click="isClick = !isClick">closs</button>
      </div>
      <draggable
        class="dragArea list-group"
        :list="todo"
        :clone="clone"
        :group="{ name: 'people', pull: pullFunction }"
        @start="start"
      >
        <div
          class="list-group-item"
          v-for="(element, index) in todo"
          :key="element.id"
        >
          <h2>id {{ element.id }}</h2>
          {{ element.name }}
          <p>C:{{ element.time }}</p>
          <h2>Last update: {{ element.you }}</h2>
          <button @click="deleteTodo(index)" class="cross">X</button
          ><button>
            <DialogComponent :inArray="todo" :index="index"></DialogComponent>
          </button>
        </div>
      </draggable>
    </div>
    <div class="box">
      <div class="flex">
        <h3>Inprogress</h3>
        <button @click="isinProgress = !isinProgress">+</button>
      </div>
      <div v-if="isinProgress" class="addedbox">
        <input v-model="progressinput" type="text" />
        <br />
        <button @click="addToProgress(progressinput)">Add</button>
        <button @click="isinProgress = !isinProgress">closs</button>
      </div>
      <draggable
        class="dragArea list-group"
        :list="inprogress"
        :clone="clone"
        :group="{ name: 'people', pull: pullFunction }"
        @start="start"
      >
        <div
          class="list-group-item"
          v-for="(element, index) in inprogress"
          :key="element.id"
        >
          <h2>id {{ element.id }}</h2>
          {{ element.name }}
          <p>C:{{ element.time }}</p>
          <h2>Last update: {{ element.you }}</h2>
          <button @click="deleteProgress(index)" class="cross">X</button
          ><button>
            <DialogComponent
              :inArray="inprogress"
              :index="index"
            ></DialogComponent>
          </button>
        </div>
      </draggable>
    </div>
    <div class="box">
      <div class="flex">
        <h3>Testing</h3>
        <button @click="istesting = !istesting">+</button>
      </div>
      <div v-if="istesting" class="addedbox">
        <input v-model="testininput" type="text" />
        <br />
        <button @click="addToTest(testininput)">Add</button>
        <button @click="istesting = !istesting">closs</button>
      </div>
      <draggable
        class="dragArea list-group"
        :list="testing"
        :clone="clone"
        :group="{ name: 'people', pull: pullFunction }"
        @start="start"
      >
        <div
          class="list-group-item"
          v-for="(element, index) in testing"
          :key="element.id"
        >
          <h2>id {{ element.id }}</h2>
          {{ element.name }}
          <p>C:{{ element.time }}</p>
          <h2>Last update: {{ element.you }}</h2>
          <button @click="deleteTest(index)" class="cross">X</button
          ><button>
            <DialogComponent
              :inArray="testing"
              :index="index"
            ></DialogComponent>
          </button>
        </div>
      </draggable>
    </div>

    <div class="box">
      <div class="flex">
        <h3>Done</h3>
        <button @click="isdone = !isdone">+</button>
      </div>
      <div v-if="isdone" class="addedbox">
        <input v-model="doneinput" type="text" />
        <br />
        <button @click="addToDone(doneinput)">Add</button>
        <button @click="isdone = !isdone">closs</button>
      </div>
      <draggable class="dragArea list-group" :list="done" group="people">
        <div
          class="list-group-item"
          v-for="(element, index) in done"
          :key="element.id"
        >
          <h2>id {{ element.id }}</h2>
          {{ element.name }}
          <p>C:{{ element.time }}</p>
          <h2>Last update: {{ element.you }}</h2>

          <!--  -->

          <v-menu offset-y>
            <template v-slot:activator="{ on, attrs }">
              <v-btn color="" v-bind="attrs" v-on="on"> ... </v-btn>
            </template>
            <v-list>
              <ul>
                <li>
                  <button @click="deleteDone(index)" class="cross">X</button>
                </li>
                <li>
                  <button>
                    <DialogComponent
                      :inArray="done"
                      :index="index"
                      :id="element.id"
                      :time="element.time"
                    ></DialogComponent>
                  </button>
                </li>
              </ul>
            </v-list>
          </v-menu>
          <!--  -->
        </div>
      </draggable>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";
import DialogComponent from "./DialogComponent.vue";
export default {
  order: 4,
  components: {
    draggable,
    DialogComponent,
  },
  data() {
    return {
      isClick: false,
      isinProgress: false,
      istesting: false,
      isdone: false,
      currentId: 9,

      todoinput: "",
      progressinput: "",
      testininput: "",
      doneinput: "",

      todo: [
        {
          name: "hello i am pallob",
          id: 1,
          time: "2022-10-08T11:18:58.196Z",
          you: "12-49-20",
        },
        {
          name: "hello i am partho",
          id: 2,
          time: "2022-10-08T11:18:58.196Z",
          you: "12-49-20",
        },
      ],
      inprogress: [
        {
          name: "hello i am John",
          id: 3,
          time: "2022-10-08T11:18:58.196Z",
          you: "12-49-20",
        },
        {
          name: "hello i am mon",
          id: 4,
          time: "2022-10-08T11:18:58.196Z",
          you: "12-49-20",
        },
      ],
      testing: [
        {
          name: "hello i am pallob",
          id: 5,
          time: "2022-10-08T11:18:58.196Z",
          you: "12-49-20",
        },
        {
          name: "hello i am partho",
          id: 6,
          time: "2022-10-08T11:18:58.196Z",
          you: "12-49-20",
        },
      ],
      done: [
        {
          name: "hello i am pallob",
          id: 7,
          time: "2022-10-08T11:18:58.196Z",
          you: "12-49-20",
        },
        {
          name: "hello i am partho",
          id: 8,
          time: "2022-10-08T11:18:58.196Z",
          you: "12-49-20",
        },
      ],
      controlOnStart: true,
    };
  },
  methods: {
    clone({ name, time, id }) {
      return { name, id, time };
    },
    pullFunction() {
      return this.controlOnStart ? "clone" : true;
    },
    start({ originalEvent }) {
      this.controlOnStart = originalEvent.ctrlKey;
    },
    addToTodo(item) {
      var date = new Date();
      var curretnTime = JSON.stringify(date);
      let obItem = {
        name: item,
        time: curretnTime,
        id: this.currentId++,
      };
      this.todo.push(obItem);
      this.isClick = false;
    },
    addToProgress(item) {
      var date = new Date();
      var curretnTime = JSON.stringify(date);
      let obItem = {
        name: item,
        time: curretnTime,
        id: this.currentId++,
      };
      this.inprogress.push(obItem);
      this.isinProgress = false;
    },
    addToTest(item) {
      var date = new Date();
      var curretnTime = JSON.stringify(date);
      let obItem = {
        name: item,
        time: curretnTime,
        id: this.currentId++,
      };
      this.testing.push(obItem);
      this.istesting = false;
    },
    addToDone(item) {
      var date = new Date();
      var curretnTime = JSON.stringify(date);
      let obItem = {
        name: item,
        time: curretnTime,
        id: this.currentId++,
      };
      this.done.push(obItem);
      this.isdone = false;
    },
    deleteTodo(id) {
      this.todo.splice(id, 1);
      console.log(id, this.todo);
    },
    deleteProgress(id) {
      this.inprogress.splice(id, 1);
    },
    deleteTest(id) {
      this.testing.splice(id, 1);
    },
    deleteDone(id) {
      this.done.splice(id, 1);
    },
  },
};
</script>
<style scoped>
.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
}
.flex {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
button {
  height: 20px;
  border: none;
  cursor: pointer;
}
.list-group-item {
  background-color: rgb(250, 246, 241);
  margin-bottom: 5px;
  padding: 10px 5px;
  border-radius: 5px;
}
.box {
  width: 300px;
}
.addedbox {
  background-color: azure;
  text-align: center;
  padding: 5px;
  margin: 10px 0;
}
input {
  width: 80%;
  padding: 10px 5px;
}
.cross {
  background-color: red;
  color: white;
  font-weight: bold;
  border-radius: 5px;
  margin-right: 10px;
}
</style>
