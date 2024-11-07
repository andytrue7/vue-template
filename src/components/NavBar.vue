<template>
  <nav>
    <Menubar class="menu" :model="items" />
  </nav>
</template>

<script>
import { Menubar } from 'primevue'

  export default {
    components: {
      Menubar,
    },

    data() {
      return {
        items: [
          {
            label: 'Alerts',
            icon: 'pi pi-bell',
          },
          {
            label: 'Knowledge Base',
            icon: 'pi pi-info-circle',
          },
          {
            label: 'Quick Links',
            icon: 'pi pi-link',
            items: [
              {
                label: 'Item1',
              }
            ]
          },
        ],
      }
    }
  }

</script>

<style scoped>
  .menu {
    border: none;
  }
</style>
