<template>
  <div class="header">
    <h3 class="heading">
      To do list 
      <span id="tasksNumber" class="tasks-numbers"> ( {{ counter }} )</span>
    </h3>
  </div>
</template>

<script>
export default {
  props: ["counter"],
};
</script>

<style scoped>
.header {
  background-color: #b80e65;
  border-radius: 5px;
}

.heading {
  padding: 15px 0 15px 15px;
  color: #fff;
  text-align: center;
  justify-content: center !important;
}

.heading span {
  margin-left: 15px;
}
</style>
