<template>
  <b-col cols="12" lg="6">
    <b-row>
      <!-- SORT : START -->
      <control-sort
        v-on:handleSort="handleSort"
        v-bind:orderBy="orderBy"
        v-bind:orderDir="orderDir"
      />
      <!-- SORT : END -->

      <!-- SEARCH : START -->
      <control-search
        v-on:handleSearch="handleSearch"
        v-bind:strSearch="strSearch"
      />
      <!-- SEARCH : END -->
    </b-row>
  </b-col>
</template>

<script>
import ControlSearch from "./ControlSearch.vue";
import ControlSort from "./ControlSort.vue";
export default {
  components: { ControlSearch, ControlSort },
  name: "comp-control",

  data() {
    return {};
  },
  props: {
    strSearch: String,
    orderBy: String,
    orderDir: String,
  },

  mounted() {},

  methods: {
    handleSearch(value) {
      this.$emit("handleSearch", value);
    },
    handleSort(data, data1) {
      this.$emit("handleSort", data, data1);
    },
  },
};
</script>

<style lang="scss" scoped>
</style>