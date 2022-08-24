<template>
  <b-col cols="12">
    <div class="input-group">
      <input
        v-on:input="handleSearch"
        v-bind:value="strSearch"
        type="text"
        class="form-control mr-2"
        placeholder="Search for..."
      />
      <span class="input-group-append">
        <button v-on:click="handleClear" class="btn btn-info" type="button">
          Clear!
        </button>
      </span>
    </div>
  </b-col>
</template>

<script>
export default {
  name: "control-search",
  props: {
    strSearch: String,
  },

  data() {
    return {};
  },

  mounted() {},

  methods: {
    handleSearch(e) {
      this.$emit("handleSearch", e.target.value);
    },
    handleClear() {
      this.$emit("handleSearch", "");
    },
  },
};
</script>

<style  scoped>
</style>