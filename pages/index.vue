<template>
  <div class="container">
    <pagination-table
      :paginationData="paginationData"
      :total="total"
      @onPageChange="onPageChange"
    />
  </div>
</template>

<script>
import Vue from "vue";
import PaginationTable from "../components/PaginationTable";
import axios from "axios";

export default Vue.extend({
  components: {
    PaginationTable,
  },
  data() {
    return {
      paginationData: [],
      total: 0,
    };
  },
  head() {
    return {
      title: "Pagination App",
    };
  },
  methods: {
    onPageChange(pageInfo) {
      this.getData(pageInfo);
    },
    async getData(pageInfo) {
      const config = {
        headers: {
          Accept: "application/json",
        },
      };
      try {
        const url =
          "https://person-app-backend.herokuapp.com/api/listPersons?start=" +
          pageInfo.start +
          "&limit=" +
          pageInfo.limit;
        const resp = await axios.get(url, config);
        this.paginationData = resp.data.persons;
        this.total = resp.data.total;
        console.log(resp);
      } catch (err) {
        console.log(err);
      }
    },
  },
});
</script>

<style>
</style>
