<template>
  <div id="toDo" class="to-do">
    <Header :counter="list.length" />
    <List @editItem="edit" @removeItem="remove" :list="list" />
    <Add :addData="addData" :editlist="editList" @childToParent="child" />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import List from "./components/List.vue";
import Add from "./components/Add.vue";
export default {
  data() {
    return {
      addData: {
        name: "",
        time: "",
      },
      list: [{ name: "Momen", time: "" }],
      editList: [],
      isEditing: false,
      editItemName: "",
    };
  },
  components: {
    Header,
    List,
    Add,
  },
  methods: {
    child(ev) {
      if (ev.name !== "") {
        // is edit or add
        if (this.isEditing) {
          this.list.forEach((item) => {
            if (item.name == this.editItemName) {
              item.name = ev.name;
            }
          });
        } else {
          // Add New Task
          let names = this.list.map((x) => x.name);
          console.log("names: ", names);
          if (names.indexOf(ev.name) == -1) {
            this.list.push({ name: ev.name, time: ev.time });
          }
        }
        this.addData.name = "";
        this.isEditing = false;

        // let isAdded = false;
        // this.list.forEach((i) => {
        //   if (i.name !== ev.name && !isAdded) {
        //     this.list.push({ name: ev.name, time: ev.time });
        //     isAdded = true;
        //   }
        // });
      }
    },
    remove(i) {
      this.list.splice(i, 1);
    },
    edit(data) {
      this.isEditing = true;
      this.editItemName = data.name;
      this.addData.name = data.name;
      this.addData.time = data.time;
    },
  },
  created() {
    let [time] = this.list;
    const date = new Date();
    time.time = new Intl.DateTimeFormat("en-GB", {
      timeStyle: "short",
    }).format(date);
  },
};
</script>

<style lang="scss">
body {
  background-color: #1c1b4d;
  font-family: Arial, Helvetica, sans-serif;
}

:focus {
  outline: none;
}

.to-do {
  width: 500px;
  margin: 100px auto;
}
</style>
