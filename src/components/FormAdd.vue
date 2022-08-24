<template>
  <div class="form-group add-task mb-3 w-100">
    <button
      v-if="!isShowForm"
      v-on:click="clickAddTask"
      type="button"
      class="btn btn-info btn-block w-100"
    >
      Add Task
    </button>
    <button
      v-if="isShowForm"
      v-on:click="clickAddTask"
      type="button"
      class="btn btn-primary btn-block w-100"
    >
      Close Task
    </button>
  </div>
</template>

<script>
export default {
  name: "form-add",
  props: { isShowForm: Boolean },

  data() {
    return {};
  },

  mounted() {},

  methods: {
    clickAddTask() {
      this.$emit("handleToggleForm");
    },
  },
};
</script>

<style scoped>
</style>