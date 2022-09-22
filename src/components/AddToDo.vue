<template lang="">
  <div class="wrapper">
    <form>
      <label>Add headline</label>
      <input type="text" v-model="inputHeadline" />
      <label>Add todo</label>
      <textarea type="text" v-model="inputInfo"></textarea>
      <button @click.prevent="submitTask" :disabled="!inputHeadline">
        Add task
      </button>
    </form>

    <table>
      <thead>
        <th>Headline</th>
        <th>Info</th>
        <th>Delete</th>
      </thead>
      <tbody>
        <tr v-for="(task, index) in taskList" :key="index">
          <td>{{ task.headline }}</td>
          <td>{{ task.info }}</td>
          <td class="pointer" @click.prevent="deleteTask(index)">
            {{ task.delete }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  emits: ["add-contact"],
  data() {
    return {
      statusInfo: ["todo", "in-progress", "done"],
      editedTask: 0,
      inputHeadline: "",
      inputInfo: "",
      taskList: [
        {
          headline: "",
          info: "",
          delete: "",
        },
      ],
    };
  },
  methods: {
    submitTask() {
      if (this.inputHeadline.length === 0) return;

      this.taskList.push({
        headline: this.inputHeadline,
        info: this.inputInfo,
        delete: "Delete",
      });

      this.inputHeadline = "";
      this.inputInfo = "";
    },
    deleteTask(index) {
      this.taskList.splice(index, 1);
    },
  },
};
</script>
<style lang="scss">
form {
  margin-top: 5rem;
  display: flex;
  flex-direction: column;
  width: 20rem;
  height: 10rem;
  justify-content: space-around;
  border: 1px solid black;
  padding: 1rem;
}

.pointer {
  cursor: pointer;
}

.wrapperCheckbox {
  display: flex;
  flex-direction: column;
}

.wrapper {
  display: flex;
  flex-direction: column;
  width: 100%;
  justify-content: center;
  align-items: center;
}

table {
  margin-top: 5rem;
  width: 20rem;

  td {
    text-align: center;
  }
}
</style>
