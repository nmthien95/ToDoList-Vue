<template>
  <b-col cols="12" lg="6">
    <!-- ADD : START -->

    <form-add
      v-bind:isShowForm="isShowForm"
      v-on:handleToggleForm="handleToggleForm"
    />
    <!-- ADD : END -->

    <form
      v-if="isShowForm"
      action=""
      method="POST"
      class="form-inline justify-content-between"
    >
      <div class="row">
        <div class="form-group mb-4 col-12">
          <input
            type="text"
            class="form-control"
            v-model="taskName"
            placeholder="Task Name"
          />
        </div>
        <div class="form-group mb-3 col-12">
          <select
            name="ds"
            v-model="level"
            class="form-control"
            required="required"
          >
            <option value="0">Small</option>
            <option value="1">Medium</option>
            <option value="2">High</option>
          </select>
        </div>
        <div class="col-6 px-3">
          <button
            v-if="taskSelected === null"
            v-on:click="handleAddNewTask"
            type="button"
            class="btn btn-primary w-100"
          >
            Submit
          </button>
          <button
            v-else
            v-on:click="handleEditTask"
            type="button"
            class="btn btn-primary w-100"
          >
            Update
          </button>
        </div>
        <div class="col-6 px-3">
          <button
            v-on:click="handleCancel"
            type="button"
            class="btn btn-secondary w-100"
          >
            Cancel
          </button>
        </div>
      </div>
    </form>
  </b-col>
</template>

<script>
import FormAdd from "./FormAdd.vue";
import { v4 as uuidv4 } from "uuid";
export default {
  components: { FormAdd },
  name: "comp-form",
  props: { isShowForm: Boolean, taskSelected: Object },

  data() {
    return { taskName: "", level: 0 };
  },

  mounted() {},
  watch: {
    // watcher taskSelected
    taskSelected: function (newData) {
      if (this.taskSelected !== null) {
        // NGười dùng có click vào button edit
        this.taskName = newData.name;
        this.level = newData.level;
      }
    },
  },
  // beforeUpdate() {
  //   // if (this.taskSelected !== null) {
  //   //   // NGười dùng có click vào button edit
  //   //   this.taskName = this.taskSelected.name;
  //   //   this.level = this.taskSelected.level;
  //   // }
  // },

  methods: {
    handleEditTask() {
      let objTaskEdit = {
        id: this.taskSelected.id,
        name: this.taskName,
        level: parseInt(this.level),
      };
      this.$emit("handleEditTaskByID", objTaskEdit);
      this.handleResetValue();
    },
    handleAddNewTask() {
      let objTask = {
        id: uuidv4(),
        name: this.taskName,
        level: parseInt(this.level),
      };
      this.$emit("handleAddNewTask", objTask);
      this.handleCancel();
    },
    handleToggleForm() {
      this.$emit("handleToggleForm");
    },
    handleCancel() {
      this.$emit("handleToggleForm");
      this.handleResetValue();
    },
    handleResetValue() {
      this.taskName = "";
      this.level = 0;
    },
  },
};
</script>

<style  scoped>
</style>
