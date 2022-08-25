<template>
  <div id="app">
    <b-container>
      <!-- TITLE : START -->
      <component-title />
      <!-- TITLE : END -->

      <b-row>
        <!-- CONTROL (SEARCH + SORT + ADD) : START -->
        <comp-control
          v-on:handleSort="handleSort"
          v-bind:orderBy="orderBy"
          v-bind:orderDir="orderDir"
          v-on:handleSearch="handleSearch"
          v-bind:strSearch="strSearch"
        />
        <!-- CONTROL (SEARCH + SORT + ADD) : END -->

        <!-- FORM : START -->
        <comp-form
          v-on:handleEditTaskByID="handleEditTaskByID"
          v-bind:taskSelected="taskSelected"
          v-on:handleAddNewTask="handleAddNewTask"
          v-on:handleToggleForm="handleToggleForm"
          v-bind:isShowForm="isShowForm"
        />
        <!-- FORM : END -->
      </b-row>

      <!-- LIST : START -->
      <todo-list-table
        v-on:handleEdit="handleEdit"
        v-on:handleDelete="handleDelete"
        v-bind:listTask="listTaskSort"
      />
    </b-container>
  </div>
</template>

<script>
import CompControl from "./components/CompControl.vue";
import CompForm from "./components/CompForm.vue";
import ComponentTitle from "./components/ComponentTitle.vue";
import TodoListTable from "./components/TodoListTable";
// import listTask from "./moks/task";

export default {
  components: { TodoListTable, ComponentTitle, CompControl, CompForm },
  name: "App",
  data() {
    return {
      listTask: null,
      isShowForm: false,
      strSearch: "",
      orderBy: "name",
      orderDir: "asc",
      taskSelected: null,
    };
  },
  watch: {
    listTask: function (newData) {
      let taskString = JSON.stringify(newData);
      localStorage.setItem("listTask", taskString);
    },
  },
  created() {
    // lấy listTask từ trong localStorage
    let tasks = localStorage.getItem("tasks");
    if (tasks !== null) {
      this.listTask = JSON.parse(tasks);
    } else {
      this.listTask = [];
    }
  },
  computed: {
    listTaskSearch() {
      let newItems = [];
      this.listTask.forEach((item) => {
        if (item.name.toLowerCase().includes(this.strSearch.toLowerCase())) {
          newItems.push(item);
        }
      });

      return newItems;
    },
    listTaskSort() {
      let listTask = [...this.listTaskSearch];

      listTask.sort(this.compareSort);

      return listTask;
    },
  },

  methods: {
    handleEditTaskByID(objTaskEdit) {
      console.log("objTaskEdit: ", objTaskEdit);
      // tìm index  tương ứng  với taskEdit.id nằm trtong listTask gốc
      const index = this.listTask.findIndex(
        (item) => item.id === objTaskEdit.id
      );
      // áp dujg splice để xóa và thêm mới gias trị vao listTask
      if (index !== -1) {
        this.listTask.splice(index, 1, objTaskEdit);
        this.handleToggleForm();
      }
    },

    handleEdit(taskEdit) {
      this.isShowForm = true;
      console.log("taskEdit: ", taskEdit);
      this.taskSelected = taskEdit;
    },
    handleAddNewTask(objTask) {
      console.log("objTask: ", objTask);
      this.listTask.push(objTask);
    },

    handleDelete(taskDelete) {
      const newItems = this.listTask.filter(
        (item) => item.id !== taskDelete.id
      );
      console.log("newItems: ", newItems);
      this.listTask = newItems;
      //cách 2 dùng spice(indexDelete,1) thay đổi mảng gốc
    },

    handleToggleForm() {
      if (this.isShowForm) this.taskSelected = null;
      this.isShowForm = !this.isShowForm;
    },
    compareSort(a, b) {
      let numberSort = this.orderDir === "asc" ? -1 : 1;
      if (a[this.orderBy] < b[this.orderBy]) return numberSort;
      else if (a[this.orderBy] > b[this.orderBy]) return numberSort * -1;
      return 0;
    },

    handleSearch(value) {
      this.strSearch = value;
    },
    handleSort(data, data1) {
      this.orderBy = data;
      this.orderDir = data1;
    },
    debounce(callback, wait) {
      let timeoutId;
      return () => {
        if (timeoutId) {
          clearTimeout(timeoutId);
        }
        timeoutId = setTimeout(callback, wait);
      };
    },
  },
};
</script>

<style>
body {
  padding: 100px 0;
}
.table > tbody > tr > td,
.table > tbody > tr > th,
.table > tfoot > tr > td,
.table > tfoot > tr > th,
.table > thead > tr > td,
.table > thead > tr > th {
  vertical-align: middle;
}

.container > .row {
  margin-top: 20px;
  margin-bottom: 30px;
}

span.badge-medium {
  padding: 11px 10px;
  margin: 0px 8px;
  font-size: 16px;
  display: inline-block;
  vertical-align: top;
}

@media (max-width: 992px) {
  .add-task {
    margin-top: 50px;
  }
}
</style>
