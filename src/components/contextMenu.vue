<template>
  <div class="context-menu" :style="{top: y + 'px', left: x + 'px'}">
    <ul>
      <li style="padding: 5px" v-for="(item, index) in items" :key="index" @click="selectItem(item)">
        {{ item.text }}
      </li>
    </ul>
  </div>
</template>

<style>
li{
  font-family: 'Montserrat', sans-serif;
  color: #9E9E9E;
  font-weight:500;
  font-size: 14px;
  word-wrap: break-word;
}

li:hover {
  color: #fff;
}

.context-menu {
  position: absolute;
  color: #fff;
  background-color: #34384e;
  width: 150px;
  height: 60px;
  border-radius: 15px;
}

ul {
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
  list-style-type: none;
}

</style>

<script>
export default {
  props: {
    items: {
      type: Array,
      required: true
    },
  },
  methods: {
    selectItem(item) {
      this.$emit('itemSelected', item);
    }
  }
}
</script>
