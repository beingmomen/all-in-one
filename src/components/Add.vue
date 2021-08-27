<template>
  <div>
    <div class="addition">
      <input
        class="task-input"
        type="text"
        name="task"
        @keyup.enter="addNew"
        placeholder="Add new task"
        v-model="addData.name"
      />
      <input
        class="current-time"
        type="time"
        name="time"
        @keyup.enter="addNew"
        v-model="addData.time"
      />
      <p class="text-light">NAme Is : {{ addData.name }}</p>
      <!-- <i id="addTask" class="add-task fas fa-plus fa-2x"></i> -->
      <font-awesome-icon
        class="add-task"
        @click="addNew"
        :icon="['fas', 'plus']"
        size="2x"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: ["editList", "addData"],
  methods: {
    addNew() {
      this.$emit("childToParent", this.addData);
      // this.addData.name = "";
    },
  },
  computed: {},
  created() {
    const date = new Date();
    this.addData.time = new Intl.DateTimeFormat("en-GB", {
      timeStyle: "short",
    }).format(date);
    // this.addData.name = this.editData.name
    // this.addData.name = this.editData.name
    // console.log(this.$props.editList);
  },
};
</script>

<style scoped>
.addition {
  position: relative;
}

.task-input {
  padding: 15px 20px;
  border: none;
  width: 100%;
  border-radius: 7px;
  margin-right: 1%;
  background-color: #002e63;
  color: #fff;
}

input:-internal-autofill-selected {
  background-color: #000;
}

.current-time {
  position: absolute;
  top: 12px;
  right: 47px;
  background-color: transparent;
  border: none;
  color: #9c9ba1;
}

.add-task {
  cursor: pointer;
  position: absolute;
  top: 10px;
  right: 10px;
  color: #9c9ba1;
}
</style>
