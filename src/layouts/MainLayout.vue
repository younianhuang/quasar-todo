<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />
        <div class="q-px-md q-py-md absolute-right">Quasar v{{ $q.version }}</div>
      </q-toolbar>
      <div class="q-mx-lg q-my-lg">
          <div class="text-h3">Todo</div>
          <div class="text-subtitle1">{{ currnetDate }}</div>
      </div>
      <q-img
        src="../assets/universe.jpg"
        class="header-image absolute-top"
        >
      </q-img>
    </q-header>

    <q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        :width="300"
        :breakpoint="900"
      >
        <q-scroll-area style="height: calc(100% - 176px); margin-top: 176px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item clickable v-ripple to="/">
              <q-item-section avatar>
                <q-icon name="list" />
              </q-item-section>

              <q-item-section>
                Todo
              </q-item-section>
            </q-item>

            <q-item active clickable v-ripple to="/help">
              <q-item-section avatar>
                <q-icon name="help" />
              </q-item-section>

              <q-item-section>
                Help
              </q-item-section>
            </q-item>
          </q-list>
        </q-scroll-area>

        <q-img class="absolute-top" src="../assets/universe.jpg" style="height: 176px">
          <div class="absolute-bottom bg-transparent">
            <q-avatar size="64px" class="q-mb-sm">
              <img src="../assets/nolan.png">
            </q-avatar>
            <div class="text-weight-bold">Nolan</div>
            <div>@github</div>
          </div>
        </q-img>
      </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { date } from 'quasar'

export default defineComponent({
  name: 'MainLayout',

  data() {
    return {
      leftDrawerOpen: false,
    }
  },

  methods: {
    toggleLeftDrawer () {
      this.leftDrawerOpen = !this.leftDrawerOpen
    }
  },

  computed: {
    currnetDate() {
      const timeStamp = Date.now()
      return date.formatDate(timeStamp, 'dddd YYYY/MM/DD')
    }
  }
});
</script>

<style lang="scss">
.header-image {
  height: 100%;
  z-index: -1;
  opacity: 0.2;
  filter: grayscale(100%);
}
</style>
