<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-img src="../assets/mountain.jpg"
        class="header-image absolute-top">
      </q-img>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title class ="text-weight-bolder q-pa-xl">
          To Do List
        </q-toolbar-title>
        <div class="text-body2 text-weight-medium">{{ todaysDate }}</div>
      </q-toolbar>
    </q-header>

      <q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        :width="250"
        :breakpoint="600"
      >
        <q-scroll-area style="height: calc(100% - 127.5px); margin-top: 150px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item 
              clickable
              exact
              v-ripple
              to="/"
              >
              <q-item-section avatar>
                <q-icon name="list"></q-icon>
              </q-item-section>

              <q-item-section>
                To Do
              </q-item-section>
            </q-item>
            <q-item
              clickable
              v-ripple
              exact
              to="/help"
              >
              <q-item-section avatar>
                <q-icon name="help"></q-icon>
              </q-item-section>

              <q-item-section>
                Help
              </q-item-section>
            </q-item>
          </q-list>
        </q-scroll-area>

        <q-img class="absolute-top" src="../assets/mountain.jpg" style="height: 127.5px;">
          <div class="absolute-bottom bg-transparent">
            <q-avatar size="56px" class="q-mb-sm">
              <img src="../assets/logo.png">
            </q-avatar>
            <div class="text-weight-bold">Miujiq Technology</div>
            <div>miujiqtech.com</div>
          </div>
        </q-img>
      </q-drawer>

    <q-page-container>
      <keep-alive>
      <router-view />
      </keep-alive>
    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from 'components/EssentialLink.vue'
import { date } from 'quasar'

const linksList = [
  {
    title: 'Docs',
    caption: 'quasar.dev',
    icon: 'school',
    link: 'https://quasar.dev'
  },
  {
    title: 'Github',
    caption: 'github.com/quasarframework',
    icon: 'code',
    link: 'https://github.com/quasarframework'
  },
  {
    title: 'Discord Chat Channel',
    caption: 'chat.quasar.dev',
    icon: 'chat',
    link: 'https://chat.quasar.dev'
  },
  {
    title: 'Forum',
    caption: 'forum.quasar.dev',
    icon: 'record_voice_over',
    link: 'https://forum.quasar.dev'
  },
  {
    title: 'Twitter',
    caption: '@quasarframework',
    icon: 'rss_feed',
    link: 'https://twitter.quasar.dev'
  },
  {
    title: 'Facebook',
    caption: '@QuasarFramework',
    icon: 'public',
    link: 'https://facebook.quasar.dev'
  },
  {
    title: 'Quasar Awesome',
    caption: 'Community Quasar projects',
    icon: 'favorite',
    link: 'https://awesome.quasar.dev'
  }
];

import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink
  },
  computed: {
    todaysDate(){
      const timeStamp = Date.now()
      return date.formatDate(timeStamp, 'dddd, DD MMMM YYYY')
    }

  },

  setup () {
    const leftDrawerOpen = ref(false)

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
})
</script>
<style lang="scss">
.header-image{
  height:100%;
  z-index: -1;
  filter: grayscale(100%);
  opacity:0.5;
}

</style>
