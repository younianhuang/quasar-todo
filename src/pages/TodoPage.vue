<template>
  <q-page class="bg-grey-4">
    <div class="q-pa-sm bg-primary">
      <q-input
        @keyup.enter="addTask"
        class="bg-white"
        placeholder="Add Task"
        v-model="newTask"
        filled
        dense>
        <template v-slot:append>
          <q-btn round dense flat icon="add" @click="addTask"/>
        </template>
      </q-input>
    </div>
    <div class="q-gutter-sm">
    <q-list separator class="bg-white">
      <!--
        Rendering a <label> tag (notice tag="label")
        so QCheckboxes will respond to clicks on QItems to
        change Toggle state.
      -->

      <q-item v-for="(task, index) in tasks" :key="task.title" tag="label" :class= "{ 'bg-blue-1': task.done }">
        <q-item-section avatar>
          <q-checkbox v-model="task.done" color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label :class= "{ 'done': task.done }" >{{task.title}}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done" side>
          <q-btn flat round color="black" icon="delete" @click.stop="deleteTask(index)"/>
        </q-item-section>
      </q-item>
    </q-list>
    </div>
    <div v-if="!tasks.length" class="text-primary text-h5 absolute-center no-task">
      <q-icon name="add_task" size="50px"/>
      <div class="text-center">No Task</div>
    </div>
  </q-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

interface Task {
  title: string,
  done: false
}

export default defineComponent({
  name: 'TodoPage',
  data() {
    return {
      newTask: '',
      tasks: new Array<Task>()
      // tasks: [
      //   {
      //     title: 'write code',
      //     done: false
      //   },
      //   {
      //     title: 'test code',
      //     done: false
      //   }
      // ]
    }
  },
  methods:
    {
      addTask():void {
        this.tasks.push(
          {
            title: this.newTask,
            done: false
          }
        )

        this.newTask = '';
      },

      deleteTask(index: number): void {
        this.$q.dialog({
        title: 'Confirm',
        message: 'Are you sure to delete this task?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        const title = this.tasks[index].title;

        this.tasks.splice(index, 1);

        this.$q.notify({
          message: `Task ${title} deleted.`,
          color: 'secondary'
        })
      })
      }
    }
})
;
</script>

<style lang="scss">
  .done {
    text-decoration: line-through;
    color: grey;
  }

  .no-task {
    opacity: 0.5;
  }
</style>
