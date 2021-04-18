<template>
  <div>
    <div class="table-view">
      <table id="paginationTable">
        <thead>
          <th>Name</th>
          <th v-for="n in 179" v-bind:key="n">test{{ n + 1 }}</th>
        </thead>
        <tbody>
          <tr v-for="r in paginationData" v-bind:key="r.Test2">
            <td>{{ r.name }}</td>
            <td v-for="n in 179" v-bind:key="n">
              {{ r["Test" + parseInt(n + 1)] }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="page-controls">
      <select class="mr" v-model="pageInfo.limit" @change="onPageSizeChange()">
        <option>10</option>
        <option>20</option>
        <option>30</option>
        <option>40</option>
        <option>50</option>
      </select>
      <span class="mr"> {{ pageInfo.start + 1 }} of {{ total }}</span>
      <span class="pagination-button" @click="onPreviousPage()"><</span>
      <span class="pagination-button" @click="onNextPage()">></span>
    </div>
  </div>
</template>

<script>
export default {
  name: "PaginationTable",
  props: { paginationData: Array, total: 0 },
  data() {
    return { pageInfo: { limit: 10, start: 0 } };
  },
  methods: {
    onPageChange() {
      this.$emit("onPageChange", this.pageInfo);
    },
    onPageSizeChange() {
      this.pageInfo.start = 0;
      this.onPageChange();
    },
    onPreviousPage() {
      if (this.pageInfo.start > 0) {
        this.pageInfo.start -= parseInt(this.pageInfo.limit);
        this.onPageChange();
      }
    },
    onNextPage() {
      let start = parseInt(this.pageInfo.start);
      let limit = parseInt(this.pageInfo.limit);
      if (start + limit < this.total) {
        this.pageInfo.start += parseInt(this.pageInfo.limit);
        this.onPageChange();
      }
    },
  },
  created() {
    this.onPageChange();
  },
};
</script>

<style>
.table-view {
  width: 100%;
  overflow: auto;
}
.mr {
  margin-right: 1em;
}
.page-controls {
  text-align: right;
  margin: 1em;
}
.pagination-button {
  cursor: pointer;
}
#paginationTable {
  font-family: Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

#paginationTable td,
#paginationTable th {
  border: 1px solid #ddd;
  padding: 8px;
}

#paginationTable tr:nth-child(even) {
  background-color: #f2f2f2;
}

#paginationTable tr:hover {
  background-color: #ddd;
}

#paginationTable th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: left;
  background-color: #000;
  color: white;
}
</style>