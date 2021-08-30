<template>
  <div id="toDo" class="to-do">
    <Header :counter="list.length" />
    <List @editItem="edit" @removeItem="remove" :list="list" />
    <Add :addData="addData" @addDataToList="addDataFunction" />
    <Popup :popup="popup" />
  </div>
</template>

<script>
import Header from "./components/todo/Header.vue";
import List from "./components/todo/List.vue";
import Add from "./components/todo/Add.vue";
import Popup from "./components/todo/Popup.vue";
export default {
  data() {
    return {
      addData: {
        name: "",
        time: "",
      },
      list: [{ name: "Momen", time: "12:12" }],
      isEditing: false,
      editItemName: "",
      popup: {
        show: false,
        name: "",
        time: ""
      },
      currentTime: ""
    };
  },
  components: {
    Header,
    List,
    Add,
    Popup,
  },
  methods: {
    addDataFunction(data) {
      if (data.name !== "") {
        // is edit or add
        if (this.isEditing) {
          this.list.forEach((item) => {
            if (item.name == this.editItemName) {
              item.name = data.name;
              item.time = data.time;
            }
          });
        } else {
          // Add New Task
          let names = this.list.map((x) => x.name);
          console.log("names: ", names);
          if (names.indexOf(data.name) == -1) {
            this.list.push({ name: data.name, time: data.time });
          }
        }
        this.addData.name = "";
        this.isEditing = false;
      }
    },
    remove(i) {
      this.list.splice(i, 1);
    },
    edit(data) {
      this.isEditing = true;
      this.editItemName = data.name;
      this.editItemTime = data.time;
      this.addData.name = data.name;
      this.addData.time = data.time;
    },
  },
  mounted() {
    setInterval(() => {
      const date = new Date();
      this.currentTime = new Intl.DateTimeFormat("en-GB", {
        timeStyle: "short",
      }).format(date)
      this.list.forEach(item => {
      if (item.time == this.currentTime) {
        this.popup.show = true
        this.popup.name = item.name
        this.popup.time = item.time
      } else {
        
      }
    })
    }, 5000);
  },
};
</script>

<style scoped lang="scss">

:focus {
  outline: none;
}

.to-do {
  width: 500px;
  margin: 100px auto;
}
</style>
