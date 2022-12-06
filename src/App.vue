<template>
  <main id="todolist">
    <h1>
      Todo List
      <span>Today i need To :</span>
    </h1>

    <transition-group name="todolist" tag="ul">
      <app-task
        v-for="(task, i) in defaultData"
        :class="{ done: task.done }"
        :key="task.description"
        :description="task.description"
        @check-task="handleCheck(i)"
      ></app-task>
    </transition-group>
    <togglebutton label="Move done items at the end?" name="todosort" />

    <p class="emptylist">Your todo list is empty.</p>

    <form name="newform" v-on:submit.prevent="addItem">
      <label for="newitem">Add to the todo list</label>
      <input type="text" name="newitem" id="newitem" v-model="currentTask" />

      <select v-model="selectedTag">
        <option v-for="tag in tagList" :value="tag" :key="tag.id">
          {{ tag.content }}
        </option>
      </select>
      <button type="submit" @click="addNewTask">Add item</button>
    </form>
  </main>
</template>

<script>
import AppTask from "@/components/app-task.vue";
export default {
  name: "App",
  components: {
    AppTask,
  },
  data: () => ({
    defaultData: [
      {
        description: "Подготовить шаблон компонента",
        tag: {
          id: 1,
          content: "Работа",
        },
        done: false,
      },
      {
        description: "Позвонить и договориться о встрече",
        tag: {
          id: 0,
          content: "Личное",
        },
        done: false,
      },
      {
        description: "js",
        tag: {
          id: 3,
          content: "Учеба",
        },
        done: false,
      },
      {
        description: "Сходить на тренировку",
        tag: {
          id: 2,
          content: "Спорт",
        },
        done: false,
      },
      {
        description: "Предложить сыграть в какую-то стратежку",
        tag: {
          id: 4,
          content: "Досуг",
        },
        done: false,
      },
    ],
    tagList: [
      {
        id: 1,
        content: "Работа",
      },
      {
        id: 0,
        content: "Личное",
      },
      {
        id: 3,
        content: "Учеба",
      },
      {
        id: 2,
        content: "Спорт",
      },
      {
        id: 4,
        content: "Досуг",
      },
    ],
    selectedTag: null,
    currentTask: null,
  }),
  methods: {
    handleCheck(i) {
      this.defaultData[i].done = !this.defaultData[i].done;
    },
    addNewTask() {
      this.defaultData.push({
        description: this.currentTask,
        tag: this.selectedTag,
        done: false,
      });
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#todolist {
  margin: 4rem auto;
  padding: 2rem 3rem 3rem;
  max-width: 500px;
  background: #67a4ab;
  color: #fff;
  box-shadow: -20px -20px 0px 0px rgba(100, 100, 100, 0.1);
}
#todolist h1 {
  /*text-align:center;*/
  font-weight: normal;
  font-size: 2.6rem;
  letter-spacing: 0.05em;
  border-bottom: 1px solid rgba(255, 255, 255, 0.3);
}
#todolist h1 span {
  display: block;
  font-size: 0.8rem;
  margin-bottom: 0.7rem;
  margin-left: 3px;
  margin-top: 0.2rem;
}

#todolist .emptylist {
  margin-top: 2.6rem;
  text-align: center;
  letter-spacing: 0.05em;
  font-style: italic;
  opacity: 0.8;
}
#todolist ul {
  margin-top: 2.6rem;
  list-style: none;
}
@keyframes strikeitem {
  to {
    width: calc(100% + 1rem);
  }
}
/* FORM */
form {
  margin-top: 3rem;
  display: flex;
  flex-wrap: wrap;
}
form label {
  min-width: 100%;
  margin-bottom: 0.5rem;
  font-size: 1.3rem;
}
form input {
  flex-grow: 1;
  border: none;
  background: #f7f1f1;
  padding: 0 1.5em;
  font-size: initial;
}
form button {
  padding: 0 1.3rem;
  border: none;
  background: #ff6666;
  color: white;
  text-transform: uppercase;
  font-weight: bold;
  border: 1px solid rgba(255, 255, 255, 0.3);
  margin-left: 5px;
  cursor: pointer;
  transition: background 0.2s ease-out;
}
form button:hover {
  background: #ff5e5e;
}
form input,
form button {
  font-family: "Quicksand", sans-serif;
  height: 3rem;
}
</style>
