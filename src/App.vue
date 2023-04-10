<template>
  <div class="main_container">
    <div STYLE="position: relative" class="inventory">
      <div class="inventory_text">
        <h2 style="margin: 25px 55px ; font-size: 18px">Инвентарь</h2>
        <div class="line"></div>
        <h2 style="margin: 25px 55px ; font-size: 18px">{{itemAmount}}/50</h2>
      </div>
      <div @dragend="dragEnd" id="droppable" @dragover.prevent @drop="drop" class="item_list">
        <div ref="item_amount" class="item_case">
          <inventory-item v-for="(item) in items" :key="item.id" :item="item"/>

        </div>
      </div>
    </div>
    <div class="equipment">
      <div class="on_player">
        <div class="human_body">
          <img style="margin: auto; display: block; margin-top: 5vh; height: 100%; " src="./assets/chelipizdrik.png">
        </div>
      </div>
      <div class="weapon_bar">
        <div class="hotkey">
          <div class="item_background"></div>
        </div>
          <div class="hotkey">
            <div id="droppable" @dragover.prevent @drop="drop" class="item_background"></div>
          </div>
        <div class="hotkey">
          <div id="droppable" @dragover.prevent @drop="drop" class="item_background"></div>
        </div>
        <div class="hotkey">
          <div id="droppable" @dragover.prevent @drop="drop" class="item_background"></div>
        </div>
        <div class="hotkey">
          <div id="droppable" @dragover.prevent @drop="drop" class="item_background"></div>
        </div>
        <div class="hotkey">
          <div id="droppable" @dragover.prevent @drop="drop" class="item_background"></div>
        </div>
        <div class="hotkey">
          <div id="droppable" @dragover.prevent @drop="drop" class="item_background"></div>
        </div>

      </div>
    </div>
  </div>

</template>

<script>
import InventoryItem from './components/inventoryItem';

export default {
  components: {
    InventoryItem,
  },

  methods: {
    drop(event) {
      event.preventDefault();
      const data = event.dataTransfer.getData("text");
      event.target.appendChild(document.getElementById(data));

    },
    dragEnd(event) {
      event.target.classList.remove("dragging");
    },
  },

  data() {
    return {
      items: [
        { value: 'revolver', label: 'Revolver', icon: "https://i.imgur.com/e9NcvzE.png", isDefault: true, list: 0, },
        { value: 'revolver_mk2', label: 'Revolver MK2', icon: "https://i.imgur.com/CIStAuI.png", isDefault: false, list: 0,  },
        { value: 'medkit', label: 'Med-kit', icon: "https://i.imgur.com/giCxxwR.png", isDefault: false, list: 2,  },
        { value: 'heavy_shotgun', label: 'Heavy shotgun', icon: "https://i.imgur.com/klCCo8o.png", isDefault: false, list: 0,  },
        { value: 'armor', label: 'Armor', icon: "https://i.imgur.com/ykMXYKG.png", isDefault: false, list: 1,  },
      ],
    }
  },

  computed: {
    listOne() {
      return this.items.filter((item) => item.list === 1)
    },
    listTwo() {
      return this.items.filter((item) => item.list === 2)
    },
  }
}

</script>

<style>

body {
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* width */
::-webkit-scrollbar {
  width: 10px;
}

/* Track */
::-webkit-scrollbar-track {
  border-radius: 10px;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: #31434e;
  height: 20%;
  border-radius: 10px;
}


* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}


h2, p{
  font-family: 'Montserrat', sans-serif;
  color: #fff;
  font-weight:500;
  word-wrap: break-word;
}

img {
  pointer-events: none;
}

.main_container {
  display: flex;
  position: absolute;
  top:0;
  bottom: 0;
  left: -1%;
  right: 0;

  border-radius:30px ;
  margin: auto;
  max-width: 120vh;
  max-height: 80vh;
}


.inventory {
  top: 0px;
  right: 0px;
  border-radius:30px;
  position: relative;
  width: 70%;
  height: 100%;
  background-color: #232635;
}
.inventory_text {
  display: flex;
}

.line {
  width: 80%;
  display: inline-block;
  text-align: center;
}

.item_showcase {
  display: inline-block;
  padding: 10px 10px;
}

.item_showcase p {
  font-size: 12px;
}

.item_list {
  overflow-y:scroll;
  margin-right: auto; /* 1 */
  margin-left:  auto; /* 1 */
  max-width: 90%; /* 2 */
  max-height: 89%;
  display: flex;
  flex-direction: row;
  /* 3 */
  padding-left:  10px; /* 3 */
}

.item_background {
  display: flex;
  justify-content: center;
  align-items: center;
  border: 1px solid #34384e;
  background-color: #232635;
  Filter: chroma();
  border-radius: 12px;
  width: 100px;
  height: 85px;
}

.equipment {
  margin-left: 10px;
  height: 100%;
  width: 50%;
  display: inline-block;
  background-color: #232635;
  position: relative;
  border-radius:30px;
}

.on_player {
  position: relative;
}

.human_body {
  position: relative;
}

.weapon_bar {
  z-index: 1;
  position: absolute;
  top: 0px;
  z-index: 1000;
  padding: 10px 14px;
}

.hotkey {
  height: 100%;
  text-align:left;
  display: flex;
  padding: 8px;
}

</style>
