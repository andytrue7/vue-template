<template>
  <header class="w-full">
    <div class="card wrapper flex justify-between p-4">
      <IconField class="flex">
        <InputIcon class="pi pi-search" />
        <InputText
          v-model="inputValue"
          placeholder="Input"
          class="border-round-2xl border-4 w-full px-2"
        />
      </IconField>
      <div class="flex">
        <NavBar />
        <div class="flex align-baseline">
          <Avatar image="https://primefaces.org/cdn/primevue/images/avatar/amyelsner.png" class="mr-2" shape="circle" />
          <span class="inline-flex flex-col items-start">
            <span class="font-bold">Spencer Witter</span>
            <span class="text-sm">Super Admin</span>
          </span>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
import NavBar from '@/components/NavBar.vue'
import { IconField, InputIcon, InputText, Avatar } from 'primevue'

export default {
  components: { InputIcon, IconField, InputText, NavBar, Avatar },

  data() {
    return {
      inputValue: '',
    }
  }
}
</script>

<style scoped></style>
