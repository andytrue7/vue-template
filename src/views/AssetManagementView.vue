<template>
  <div class="w-full bg-gray-50 p-16 h-full flex-grow">
    <TitleContent :title="title"/>
    <div class="card p-8 bg-white rounded-2xl">
      <div class="flex justify-between">
        <SelectButton
          v-model="value"
          :options="options"
        />
        <Button
          class="bg-sky-800 text-xs text-white rounded-2xl px-6 py-2"
        >
          + Add Item
        </Button
        >
      </div>
      <DataTable :value="itemsDemo" tableStyle="min-width: 50rem">
        <Column
          v-for="col in columns"
          :key="col.field"
          :field="col.field"
          :header="col.header"
        >
        </Column>
      </DataTable>
      <div class="flex justify-between align-baseline mt-8">
        <p class="self-center">Showing 1 to 10 of 8000 Entries</p>
        <Paginator :rows="rows" :totalRecords="totalRecords"></Paginator>
      </div>
    </div>
  </div>
</template>

<script>
import TitleContent from '@/components/TitleContent.vue'
import DataTable from 'primevue/datatable'
import SelectButton from 'primevue/selectbutton'
import Paginator from 'primevue/paginator'
import Column from 'primevue/column'

const url = import.meta.env.BASE_URL
export default {
  components: {
    Column,
    Paginator,
    SelectButton,
    DataTable,
    TitleContent,
  },
  data() {
    return {
      itemsDemo: [],
      value: 'Items',
      options: ['Items', 'Models', 'Categories'],
      columns: [],
      title: 'Asset management',
      rows: 10,
      totalRecords: 120,
    }
  },

  watch: {
    value(newValue) {
      this.fetchData(newValue)
    },
  },

  mounted() {
    this.fetchData()
  },

  methods: {
    async fetchData(resourcePath = 'Items') {
      const resourcePathToLower = resourcePath.toLowerCase()
      const response = await fetch(
        url + `api/asset-management/${resourcePathToLower}.json`,
      )
      const itemsDemo = await response.json()
      this.setItemsDemo(itemsDemo)
    },

    setItemsDemo(itemsDemo) {
      this.itemsDemo = [...itemsDemo]

      if (typeof this.itemsDemo[0] !== 'object') {
        this.itemsDemo = this.itemsDemo.map(item => ({ category: item }))
      }
      this.createColumnsFields()
    },

    createColumnsFields() {
      this.columns = [...Object.keys(this.itemsDemo[0])].map(item => {
        return { field: item, header: this.formatHeader(item) }
      })
    },

    formatHeader(field) {
      return field
        .replace(/([A-Z])/g, ' $1')
        .replace(/^./, str => str.toUpperCase())
    },
  },
}
</script>
<style scoped>
</style>
