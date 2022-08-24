<template>
  <b-col cols="12" class="mb-3">
    <div class="form-group">
      <div>
        <b-dropdown text="Sort By" class="m-2 mb-2">
          <b-dropdown-item v-on:click="handleSort('name', 'asc')"
            >Name ASC</b-dropdown-item
          >
          <b-dropdown-item v-on:click="handleSort('name', 'desc')"
            >Name DESC</b-dropdown-item
          >

          <b-dropdown-divider />
          <b-dropdown-item v-on:click="handleSort('level', 'asc')"
            >Level ASC</b-dropdown-item
          >
          <b-dropdown-item v-on:click="handleSort('level', 'desc')"
            >Level DESC</b-dropdown-item
          >
        </b-dropdown>
        <b-button class="order" variant="success"
          >{{ orderBy }} - {{ orderDir }}</b-button
        >
      </div>
    </div>
  </b-col>
</template>

<script>
export default {
  name: "control-sort",
  props: {
    orderBy: String,
    orderDir: String,
  },

  data() {
    return {};
  },

  mounted() {},

  methods: {
    handleSort(orderBy, orderDir) {
      this.$emit("handleSort", orderBy, orderDir);
    },
  },
};
</script>

<style scoped>
.order {
  text-transform: uppercase;
}
</style>