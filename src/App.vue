<template>
  <div class="main_container">
    <div class="inventory">
      <div class="inventory_text">
        <h2 style="margin: 25px 55px ; font-size: 18px">Инвентарь</h2>
        <div class="line"></div>
        <h2 style="margin: 25px 55px ; font-size: 18px">{{item_amount}}/50</h2>
      </div>
      <div class="item_list">
        <div ref="item_amount" class="item_case">
          <div  :key="index" @click="showMenu(index)" :class="{ active: selectedItemIndex === index }" class="item_showcase">
            <div class="item_background">
              <img style='height: 100%; width: 100%; object-fit: contain' src="./assets/revolver.png">
            </div>
            <p style="text-align: center; padding: 10px">{{ index }}: {{ item }}</p>
              <div ref="container">
                <ContextMenu v-if="menuVisible" :items="menuItems"/>
              </div>
          </div>
          <div class="item_showcase">
            <div class="item_background">
              <img style='height: 70%; width: 70%; object-fit: contain' src="./assets/medkit.png">
            </div>
            <p style="text-align: center; padding: 10px">Med-kit</p>
          </div>
          <div v-for="(item, index) in menuItems" :key="index" @click="showMenu(index)" :class="{ active: selectedItemIndex === index }" class="item_showcase">
            <div class="item_background">
              <img style='height: 100%; width: 70%; object-fit: contain' src="./assets/revolver_mk2.png">
            </div>
            <p style="text-align: center; padding: 10px">Revolver MK2</p>
            <div ref="container">
              <ContextMenu v-if="menuVisible" :items="menuItems"/>
            </div>
          </div>
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
          <div class="item_background"></div>
        </div>
        <div class="hotkey">
          <div class="item_background"></div>
        </div>
        <div class="hotkey">
          <div class="item_background"></div>
        </div>
        <div class="hotkey">
          <div class="item_background"></div>
        </div>
        <div class="hotkey">
          <div class="item_background"></div>
        </div>
        <div class="hotkey">
          <div class="item_background"></div>
        </div>

      </div>
    </div>
  </div>

</template>

<script>
import ContextMenu from './components/contextMenu';

export default {
  name: 'App',
  components: {
    ContextMenu
  },

  data() {
    return {
      item_amount: 0,
      menuVisible: false,
      selectedItem: '',
      selectedItemIndex: null,
      menuItems: [
        { text: 'Использовать' },
        { text: 'Выбросить' },
      ],
      items: [
        {
          id: 0,
          name: "Revolver",
          avatar: "./assets/revolver.png",
          isDefaulte: true,
        },
        {
          id: 1,
          name: "Revolver MK2",
          avatar: "./assets/revolver_mk2.png",
          isDefaulte: false,
        },
        {
          id: 3,
          name: "Steve Jobs",
          avatar: "https://pickaface.net/gallery/avatar/Opi51c74d0125fd4.png"
        },
        {
          id: 4,
          name: "Yassine Smith",
          avatar: "https://pickaface.net/gallery/avatar/unr_yassine_191124_2012_3gngr.png"
        },
        {
          id: 5,
          name: "Senior Saez",
          avatar: "https://pickaface.net/gallery/avatar/elmedinilla541c03412955c.png"
        }
      ]}
    },

  methods: {
    showMenu(index) {
      if (this.selectedItemIndex === index) {
        // Close the selected menu if it's already open
        this.menuVisible = false;
        this.selectedItemIndex = null;
      } else {
        // Close any previously opened menu
        this.menuVisible = false;

        // Open the selected menu
        this.selectedItemIndex = index;
        this.menuVisible = true;
        this.selectedItem = this.menuItems[index];

      }
    },
    hideMenu(event) {
      if (!event.target.closest('.item_showcase') && !event.target.closest('.item_showcase')) {
        this.menuVisible = false;
        this.selectedItemIndex = null;
      }
    }
  },

  mounted() {
    let item_amount = this.$refs.item_amount.getElementsByClassName('item_showcase');
    this.item_amount = item_amount.length;
      this.items.forEach((item, index) => {
        console.log(index);
      });
  },

  beforeUnmount() {
    document.removeEventListener('click', this.hideMenu);
  },

  computed: {


  },

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
