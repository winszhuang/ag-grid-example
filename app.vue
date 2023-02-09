<script setup lang="ts">
import { AgGridVue } from 'ag-grid-vue3'
import "ag-grid-community/styles/ag-grid.css";
import "ag-grid-community/styles/ag-theme-alpine.css";

interface RowData {
  make: string,
  model: string,
  price: number
}

interface ColumnDef {
  field: string,
  sortable: boolean,
  filter: boolean
}

const columnDefs = ref<ColumnDef[]>([
  { field: 'make', sortable: true, filter: true },
  { field: 'model', sortable: true, filter: true },
  { field: 'price', sortable: true, filter: true },
])

const rowData = ref<RowData[]>([
  { make: 'Vauxhall', model: 'Corsa', price: 17300 },
  { make: 'Ford', model: 'Fiesta', price: 18000 },
  { make: 'Volkswagen', model: 'Golf', price: 26000 },
])

async function fetchLargeData() {
  const { data, error } = await useFetch('https://www.ag-grid.com/example-assets/row-data.json')
  if (!error.value) {
    rowData.value = data.value as unknown as RowData[]
  } else {
    alert('Failed to get data!!')
  }
}

</script>

<template>
  <div>
    <button @click="fetchLargeData">
      click me to fetch large data
    </button>
    <div>
      <ag-grid-vue 
        :columnDefs="columnDefs"
        :rowData="rowData"
        class="ag-theme-alpine"
        style="height: 500px"
        rowSelection="multiple"
        animateRows="true"
      />
    </div>
  </div>
</template>
