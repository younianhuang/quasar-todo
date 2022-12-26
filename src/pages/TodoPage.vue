<template>
  <q-page class="bg-grey-4">
    <div class="q-gutter-sm">
    <q-list separator class="bg-white">
      <!--
        Rendering a <label> tag (notice tag="label")
        so QCheckboxes will respond to clicks on QItems to
        change Toggle state.
      -->

      <q-item v-for="todo in todos" :key="todo.title" tag="label" :class= "{ 'done': todo.done }">
        <q-item-section avatar>
          <q-checkbox v-model="todo.done" color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{todo.title}}</q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
    </div>
  </q-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'TodoPage',
  data() {
    return {
      color: true,
      todos: [
        {
          title: 'write code',
          done: false
        },
        {
          title: 'test code',
          done: false
        }
      ]
    }
  }
});
</script>

<style lang="scss">
  .done {
    text-decoration: line-through;
    color: grey;
    background-color: $blue-1;
  }
</style>
