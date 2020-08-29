<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="bg-deep-purple">
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

        <q-toolbar-title>
          Minhas Tarefas
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-1"
    >
      <q-list>
        <q-item-label header class="text-grey-8">
          Configurações
        </q-item-label>
        <!-- <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        /> -->
        <q-toggle
          v-model="value"
          label="Dark Mode"
          class="text-grey-8"
          @input="toggleDarkMode()"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
// import EssentialLink from 'components/EssentialLink.vue'

export default {
  name: 'MainLayout',
  components: {},
  data() {
    return {
      leftDrawerOpen: false,
      value: false
    }
  },
  methods: {
    toggleDarkMode() {
      this.$q.dark.toggle()
      localStorage.setItem('darkMode', this.value)
    }
  },
  created() {
    const darkMode = localStorage.getItem('darkMode')
    if (darkMode === 'true') {
      this.$q.dark.toggle()
      this.value = darkMode
    }
  }
}
</script>
