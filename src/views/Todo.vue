<template>
  <div class="home">
    <v-text-field
      v-model="newTaskTitle"
      @click:append="addTask"
      @keyup.enter="addTask"
      class="pa-4"
      outlined
      label="Add Tasks"
      hide-details
      maxlength="30"
      clearable
      append-icon="mdi-plus"
    ></v-text-field>
    <v-alert
      class="mx-6"
      v-model="alert"
      dismissible
      color="red"
      border="left"
      elevation="2"
      colored-border
      icon="mdi-alert"
    >
      Please Enter a Todo Title
    </v-alert>
    <v-list class="pt-0" flat>
      <div v-for="task in tasks" :key="task.id">
        <v-list-item
          @click="doneTask(task.id)"
          :class="{ 'blue lighten-5': task.done }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through': task.done }"
                >{{ task.title }}</v-list-item-title
              >
            </v-list-item-content>
            <v-list-item-action>
              <v-btn icon @click.stop="deleteTask(task.id)">
                <v-icon color="red lighten-1">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider class="mx-4"></v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      alert: false,
      newTaskTitle: "",
      tasks: [
        // {
        //   id: 1,
        //   title: "Eat you",
        //   done: false,
        // },
        // {
        //   id: 2,
        //   title: "Kiss you",
        //   done: false,
        // },
        // {
        //   id: 3,
        //   title: "Bite you",
        //   done: false,
        // },
      ],
    };
  },
  methods: {
    addTask() {
      let newTask = {
        id: Date.now(),
        title: this.newTaskTitle,
        done: false,
      };
      if (this.newTaskTitle == "") {
        this.alert = true;
      } else {
        this.tasks.push(newTask);
        this.newTaskTitle = "";
      }
    },
    doneTask(id) {
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.done = !task.done;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
  },
};
</script>
