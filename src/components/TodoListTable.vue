<template>
  <div>
    <div class="card panel-success">
      <div class="card-header">List Task</div>
      <table class="table table-hover">
        <thead>
          <tr>
            <th style="width: 10%" class="text-center">#</th>
            <th>Task</th>
            <th style="width: 20%" class="text-center">Level</th>
            <th style="width: 160px">Action</th>
          </tr>
        </thead>

        <tbody v-if="listTask.length !== 0">
          <todo-list-item
            v-on:handleDelete="handleDelete"
            v-on:handleEdit="handleEdit"
            v-bind:index="index"
            v-bind:task="task"
            v-for="(task, index) in listTask"
            v-bind:key="task.id"
          />
        </tbody>
        <tbody v-else>
          <tr>
            <td colspan="4"><h3>List Empty</h3></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import TodoListItem from "./TodoListItem.vue";
export default {
  name: "todo-list-table",
  props: { listTask: Array },

  data() {
    return {};
  },
  components: {
    TodoListItem,
  },

  mounted() {},

  methods: {
    handleEdit(task) {
      this.$emit("handleEdit", task);
    },
    handleDelete(data) {
      this.$emit("handleDelete", data);
    },
  },
};
</script>

<style lang="scss" scoped>
</style>