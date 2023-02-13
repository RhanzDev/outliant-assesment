<template>
    <div elevated class="main-header">
      <q-toolbar>
        <div class="logo">Logo <span></span></div>
        <div class="menus">
            <div class="menu-item" :class="$route.name === 'home' ? 'active' : ''" @click="this.$router.push({name: 'home'})">Home</div>
            <div class="menu-item" :class="$route.name === 'about' ? 'active' : ''" >About</div>
            <div class="menu-item" :class="$route.name === 'services' ? 'active' : ''">Services</div>
            <div class="menu-item" :class="$route.name === 'products' ? 'active' : ''" @click="this.$router.push({name: 'products'})"> Products</div>
        </div>
        <div class="action-button">
            <q-btn no-caps flat label="Call to Action"/>
        </div>
        <q-btn
          class="drawer_button"
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer()"
        />
      </q-toolbar>
    </div>
</template>

<script>
export default
{
    filters: { },
    data:() =>(
    {
    }),
    mounted() { },
    methods: 
    { 
      toggleLeftDrawer() 
      {
        this.$emit('openDrawer');
      }
    },
    computed: { }
}
</script>