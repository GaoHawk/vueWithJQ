<template>
  <div id="main">
  <ag-grid-vue style="width: 620px; height: 500px;"
                 class="ag-theme-balham"
                 :gridOptions="gridOptions"
                 :columnDefs="columnDefs"
                 :rowData="rowData"
                 :enableSorting="true"
                 :enableFilter="true"
                  :localeText = "localeText"
                  rowSelection="multiple"
             >
    </ag-grid-vue>
  </div>
</template>

<script>
import { AgGridVue } from "ag-grid-vue";
export default {
  name: "app",
  data() {
    return {
      gridOptions: {},
      columnDefs: null,
      rowData: null,
      localeText: {
        sum: "汇总",
        equals: "等于"
      }
    };
  },
  components: {
    "ag-grid-vue": AgGridVue
  },
  beforeMount() {
    this.columnDefs = [
      {
        headerName: "Make",
        field: "make",
        cellStyle: { width: "auto" },
        checkboxSelection: true
      },
      { headerName: "Model", field: "model", cellStyle: { width: "auto" } },
      { headerName: "Price", field: "price", cellStyle: { width: "auto" } }
    ];

    fetch("https://api.myjson.com/bins/15psn9")
      .then(result => result.json())
      .then(rowData => (this.rowData = rowData));
  }
};
</script>

<style scoped>

</style>
