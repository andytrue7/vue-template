<template>
  <div class="title-wrapper flex justify-between">
    <div class="flex mb-4">
      <i class="pi pi-mobile text-blue-700 pr-4 text-3xl" style="font-size: 1.5rem"></i>
      <p class="text-3xl">{{ title }}</p>
    </div>
    <Breadcrumb class="breadcrumb" :home="home" :model="items">
      <template #item="{ item, props }">
        <router-link v-if="item.route" v-slot="{ href, navigate }" :to="item.route" custom>
          <a :href="href" v-bind="props.action" @click="navigate">
            <span class="text-primary font-semibold">{{ item.label }}</span>
          </a>
        </router-link>
        <a v-else :href="item.url" :target="item.target" v-bind="props.action">
          <span class="text-blue-400 underline">{{ item.label }}</span>
        </a>
      </template>
    </Breadcrumb>
  </div>
</template>

<script>

import { Breadcrumb } from 'primevue'

export default {
  components: {
    Breadcrumb,
  },

  props: {
    title: {
      type: String,
      required: true,
    }
  },

  data() {
    return {
      items: [
        { label: 'Inventory' },
        { label: 'Asset Management' },
      ],
    }
  }
}
</script>

<style scoped>
  .breadcrumb {
    background: none;
    color: cornflowerblue;
  }
</style>
