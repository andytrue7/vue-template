<template>
  <!-- ignore side panel -->
  <main class="page">
    <!-- update the header -->
    <div class="flex w-full flex-col min-h-screen">
      <BaseHeader />
      <RouterView />
      <BaseFooter />
    </div>

    <!-- add the footer from design -->
  </main>
</template>

<script>
import { defineComponent } from 'vue'
import BaseHeader from '@/components/BaseHeader.vue'
import BaseFooter from '@/components/BaseFooter.vue'

export default defineComponent({
  components: { BaseFooter, BaseHeader }
})
</script>

<style scoped>
.page {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
