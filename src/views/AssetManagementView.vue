<template>
  <div class="w-full bg-gray-50 p-16 h-full flex-grow">
    <TitleContent :title="title"/>
    <div class="card p-8 bg-white rounded-2xl border-2">
      <div class="flex justify-between mb-4 h-24">
        <SelectButton
          v-model="value"
          :options="options"
          :pt="{ root: { style: 'border: 1px solid #BDBFC1' } }"
          class="h-12"
        />
        <Button
          class="bg-sky-800 text-xs text-white rounded-2xl px-6 py-3 self-end"
        >
          <i class="pi pi-plus pr-1" />
          Add Item
        </Button
        >
      </div>
      <DataTable :value="paginatedData" :rows="rows" tableStyle="min-width: 50rem" :pt="{ headerRow: { style: 'border: 3px solid #BDBFC1;' } }">
        <Column
          v-for="col in columns"
          :key="col.field"
          :field="col.field"
          :header="col.header"
          sortable
          :pt="{ headerCell: { style: 'background: #E9F0F4;' } }"
        >
        </Column>
      </DataTable>
      <div class="flex justify-between align-baseline mt-8">
        <p class="self-center">Showing {{ firstRecord }} to {{ last }} of {{ totalRecords }} Entries</p>
        <Paginator :rows="rows" :totalRecords="totalRecords" @page="onPageChange" template="PrevPageLink PageLinks NextPageLink"></Paginator>
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
      paginatedData: [],
      value: 'Items',
      options: ['Items', 'Models', 'Categories'],
      columns: [],
      title: 'Asset management',
      firstRecord: 0,
      last: 0,
      rows: 10,
      totalRecords: 0,
    }
  },

  watch: {
    value: {
      handler(newValue) {
        this.fetchData(newValue);
      },
      immediate: true,
    },
  },

  methods: {
    async fetchData(resourcePath = 'Items') {
      const resourcePathToLower = resourcePath.toLowerCase()
      const response = await fetch(
        url + `api/asset-management/${resourcePathToLower}.json`,
      )
      const itemsDemo = await response.json();
      this.setItemsDemo(itemsDemo);
      this.updatePaginatedData();
    },

    onPageChange(e) {
      this.firstRecord = e.first;
      this.updatePaginatedData();
    },

    updatePaginatedData() {
      const first = this.firstRecord;
      this.last = first + this.rows;
      this.paginatedData = this.itemsDemo.slice(first, this.last);
    },

    setItemsDemo(itemsDemo) {
      this.itemsDemo = [...itemsDemo]

      if (typeof this.itemsDemo[0] !== 'object') {
        this.itemsDemo = this.itemsDemo.map(item => ({ category: item }))
      }
      this.createColumnsFields()
      this.totalRecords = this.itemsDemo.length;
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
