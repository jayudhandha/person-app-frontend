<template>
  <div>
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
</template>

<script>
export default {
  name: "PaginationControl",
  props: {
    pageInfo: { limit: 10, start: 0 },
    total: 0,
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
};
</script>

<style>
</style>