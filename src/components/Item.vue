<template>
  <div>
    <li class="item" v-for="(item, i) in list" :key="i">
      <span class="span-name">{{ item.name }}</span>
      <span class="span-time">{{ item.time }}</span>
      <font-awesome-icon
        @click="edit(item.name, item.time, i)"
        class="edit right"
        :icon="['fas', 'edit']"
      />
      <font-awesome-icon
        @click="remove(i)"
        class="remove right"
        :icon="['fas', 'times']"
      />
    </li>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: ["list"],
  methods: {
    remove(i) {
      let result = confirm("Want to delete?");
      if (result) {
        this.$emit("removeItem", i);
      }
    },
    edit(name, time, i) {
      this.$emit("editItem", { name, time, i });
    },
  },
};
</script>

<style scoped>
.to-do .list li {
  padding: 15px 20px;
  margin-bottom: 10px;
  border-radius: 5px;
  color: #fff;
  display: block;
  background-color: #423a6f;
  list-style: none;
  position: relative;
}

.to-do .list li .right {
  position: absolute;
  cursor: pointer;
}

.to-do .list li .right.remove {
  right: 15px;
  top: 20px;
}

.to-do .list li .right.edit {
  right: 40px;
  top: 20px;
}

.to-do .list .span-time {
  position: absolute;
  right: 70px;
  top: 17px;
  color: #fff;
}
</style>
