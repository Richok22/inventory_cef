<template>
  <div class="context-container">
    <ul class="context-menu">
      <li v-for="item in items" :key="item.id" @click="item.action">{{ item.label }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    items: {
      type: Array,
      required: true,
    },
  },

};
</script>

<style scoped>
.context-menu {
  margin-top: 4px;
  position: absolute;
  z-index: 1000;
  background-color: #35374f;
  color: #9b9da9;
  border-radius: 10px;
  list-style-type: none;
  justify-content: center;
  align-items: center;
  display: flex;
  flex-direction: column;
  font-family: 'Montserrat', sans-serif;
}

li {
  font-size: 13px;
  margin: 7px;
}
li:hover {
  color:#ffffff;
}




</style>