<template>
  <nav class="filter-nav">
    <button @click="udpateFilter('all')" :class="{ active: current === 'all' }">
      View All
    </button>
    <button
      @click="udpateFilter('completed')"
      :class="{ active: current === 'completed' }"
    >
      Completed
    </button>
    <button
      @click="udpateFilter('ongoing')"
      :class="{ active: current === 'ongoing' }"
    >
      Ongoing
    </button>
  </nav>
</template>

<script>
export default {
  props: ["current"],
  methods: {
    udpateFilter(by) {
      this.$emit("filterChange", by);
    }
  },
};
</script>

<style>
.filter-nav {
  text-align: left;
}
.filter-nav button {
  background: none;
  border: none;
  color: #bbb;
  outline: none;
  font-size: 12px;
  text-transform: uppercase;
  margin-right: 10px;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
}
.filter-nav button.active {
  color: #555;
}
</style>