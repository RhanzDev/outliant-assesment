<template>
  <q-layout view="lHh Lpr lFf">
    <main-header @openDrawer="openDrawer" class="wrapper"/>

    <q-drawer
      v-model="leftDrawerOpen"
      bordered
      :breakpoint="1500" 
      :width="300"
      side="right"
    >
      <q-list>
        <template v-for="(menuItem, index) in linksList" :key="index">
          <q-item clickable :active="menuItem.route === $route.name" v-ripple @click="this.$router.push({name: menuItem.route})">
            <q-item-section avatar>
              <q-icon :name="menuItem.icon" />
            </q-item-section>
            <q-item-section>
              {{ menuItem.title }}
            </q-item-section>
          </q-item>
          <q-separator :key="'sep' + index"  v-if="menuItem.separator" />
        </template>
      </q-list>
    </q-drawer>

    <q-page-container class="wrapper">
      <router-view />
    </q-page-container>
    <main-footer />
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'
import MainHeader from 'src/pages/global/MainHeader.vue'
import MainFooter from 'src/pages/global/MainFooter.vue'
// import EssentialLink from 'components/EssentialLink.vue'
import scss from '../styles/styles.scss'



export default defineComponent({
  name: 'MainLayout',

  components: { MainHeader, MainFooter },
  data:() =>(
  {
    leftDrawerOpen: false,
    linksList: 
    [
      {

        title: 'Home',
        route: 'home',
        icon: 'home',
      },
      {
        title: 'about',
        route: ' ',
        icon: 'info',
      },
      {
        title: 'Services',
        route: ' ',
        icon: 'design_services',
      },
      {
        title: 'Products',
        route: 'products',
        icon: 'shopping_cart',
        separator: true,
      },
      {
        title: 'Call to Action',
        route: '',
        icon: 'call_to_action'
      },
    ]
  }),
  methods: 
  { 
    openDrawer() 
    {
      this.leftDrawerOpen = !this.leftDrawerOpen;
    }
  },

})
</script>
