<template>
  <div class="home">
    <v-text-field
    v-model="title"
      class="pa-3"
      label="Add Task"
      append-icon="mdi-plus"
      hide-details
      clearable
      outlined
      dense
      @click:append="addTask()"
      @keyup.enter="addTask()"
    ></v-text-field>
    <v-list flat class="pa-0">
      <div v-for="task in tasks" :key="task.id">
        <v-list-item
          :class="{ 'blue lighten-5': task.done }"
          @click="taskDone(task.id)"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox color="primary" :input-value="task.done"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content
              :class="{ 'text-decoration-line-through': task.done }"
            >
              <v-list-item-title>{{ task.title }}</v-list-item-title>
            </v-list-item-content>
            <v-list-item-action>
              <v-btn icon @click.stop="taskDelete(task.id)">
                <v-icon color="red"> mdi-delete </v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider> </v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      title:"",
      tasks: [
        {
          id: 1,
          title: "Wake Up",
          done: false,
        },
        {
          id: 2,
          title: "Do breakfast",
          done: false,
        },
        {
          id: 3,
          title: "Go to Office",
          done: false,
        },
      ],
    };
  },
  methods: {
    addTask(){
      let newTask = {
        id : Date.now(),
        title: this.title,
        done: false
      };
      this.tasks.push(newTask);
      this.title = ""
    },
    taskDone(id) {
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.done = !task.done;
    },
    taskDelete(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
  },
};
</script>

