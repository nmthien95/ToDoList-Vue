<template>
  <tr>
    <td class="text-center">{{ index }}</td>
    <td>
      {{ task.name }}
    </td>
    <td class="text-center">
      <span class="badge" v-bind:class="getClassLevel">{{ getLevelName }}</span>
    </td>
    <td>
      <b-button
        v-on:click="handleEdit"
        type="button"
        class="btn btn-primary me-2"
        >Edit</b-button
      >
      <b-button v-on:click="handleDelete" type="button" class="btn btn-danger">
        Delete
      </b-button>
    </td>
  </tr>
</template>

<script>
import mapLevel from "../moks/level";
export default {
  name: "todo-list-item",
  props: { task: Object, index: Number },
  computed: {
    getLevelName() {
      return this.mapLevel[this.task.level].name;
    },
    getClassLevel() {
      return this.mapLevel[this.task.level].levelClass;
    },
  },

  data() {
    return { mapLevel: mapLevel };
  },
  // created() {
  //   console.log("todolistItem", mapLevel);
  // },

  methods: {
    handleEdit() {
      this.$emit("handleEdit", this.task);
    },
    handleDelete() {
      if (confirm("Bạn có muốn xóa task có tên là " + this.taskName)) {
        this.$emit("handleDelete", this.task);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
</style>