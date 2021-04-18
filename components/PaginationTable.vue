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
  </div>
</template>

<script>
export default {
  name: "PaginationTable",
  props: { paginationData: Array },
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