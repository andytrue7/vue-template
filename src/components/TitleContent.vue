<template>
  <div class="title-wrapper flex justify-between">
    <div class="flex mb-4">
      <InputIcon class="pi pi-mobile text-blue-700 text-2xl pr-4" />
      <p class="text-2xl">{{ title }}</p>
    </div>
    <Breadcrumb class="breadcrumb" :home="home" :model="items">
      <template #item="{ item, props }">
        <router-link v-if="item.route" v-slot="{ href, navigate }" :to="item.route" custom>
          <a :href="href" v-bind="props.action" @click="navigate">
            <span class="text-primary font-semibold">{{ item.label }}</span>
          </a>
        </router-link>
        <a v-else :href="item.url" :target="item.target" v-bind="props.action">
          <span class="text-blue-400 underline  dark:text-surface-0">{{ item.label }}</span>
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
