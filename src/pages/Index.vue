<template>
  <q-page class="flex flex-center">
    <div class="text-h3 q-mt-lg">Tarefas</div>
    <TasksProgress class="q-mt-lg" v-if="tasks.length" :progress="progress" />
    <NewTask @taskAdded="addTask" />
    <TaskGrid
      :tasks="tasks"
      @taskDeleted="deleteTask"
      @taskStateChanged="toggleTaskState"
    />
  </q-page>
</template>

<script>
import TasksProgress from 'src/components/TaskProgress.vue'
import NewTask from 'src/components/NewTask.vue'
import TaskGrid from 'src/components/TaskGrid.vue'

export default {
  components: { TasksProgress, NewTask, TaskGrid },
  name: 'PageIndex',
  data() {
    return {
      tasks: []
    }
  },
  computed: {
    progress() {
      const total = this.tasks.length
      const done = this.tasks.filter(t => !t.pending).length
      return Math.round((done / total) * 100) || 0
    }
  },

  watch: {
    tasks: {
      deep: true,
      handler() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks))
      }
    }
  },

  methods: {
    addTask(task) {
      const sameName = t => t.name === task.name
      const reallyNew = this.tasks.filter(sameName).length === 0
      if (reallyNew) {
        this.tasks.push({
          name: task.name,
          pending: task.pending || true
        })
      }
    },

    deleteTask(i) {
      this.tasks.splice(i, 1)
    },

    toggleTaskState(i) {
      this.tasks[i].pending = !this.tasks[i].pending
    }
  },

  created() {
    const json = localStorage.getItem('tasks')
    const array = JSON.parse(json)
    this.tasks = Array.isArray(array) ? array : []
  }
}
</script>
