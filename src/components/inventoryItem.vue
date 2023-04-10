  <template>
      <div id="draggable"
           draggable="true"
           @dragstart="dragStart" class="item_showcase">
        <div class="item_background" @contextmenu.prevent="showContextMenu">
          <img  style='height: 70%; width: 70%; object-fit: contain' :src="item.icon">
        </div>
        <p style="text-align: center ; padding: 10px">{{item.label}}</p>
        <context-menu :items="menuItems" v-if="showMenu" @click="hideContextMenu" />
      </div>
</template>

<script>
import contextMenu from "@/components/contextMenu";
export default {
  components: {
    contextMenu,
  },
  props: {
    item: {
      type: Object,
      isDefault: false,
    }
  },
  data() {
    return {
      showMenu: false,
      drag: false,
      itemAmount: 0,
      menuItems: [
        {
          id: 1,
          label: "Использовать",
          action: () => {
            console.log("Menu item 1 clicked");
          },
        },
        {
          id: 2,
          label: "В быстрый слот",
          action: () => {
            console.log("Menu item 2 clicked");
          },
        },
        {
          id: 3,
          label: "Выбросить",
          action: () => {
            console.log("Menu item 3 clicked");
          },

        },
      ],
    };
  },
  methods: {
    showContextMenu(event) {
      event.preventDefault();
      this.showMenu = true;
    },
    hideContextMenu() {
      this.showMenu = false;
    },
    dragStart(event) {
      event.dataTransfer.setData("text", event.target.id);
      event.target.classList.add("dragging");
      this.showMenu = false;
    },

    drop(event) {
      event.preventDefault();
      const data = event.dataTransfer.getData("text");
      event.target.appendChild(document.getElementById(data));
      event.target.classList.add("hotkey");

    },
    dragEnd(event) {
      event.target.classList.remove("dragging");
    },
  },

  computed: {
    listOne() {
      return this.items.filter((item) => item.list === 1)
    },
    listTwo() {
      return this.items.filter((item) => item.list === 2)
    },
  },

}

</script>

<style>
. {
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


.item_showcase {
  display: inline-block;
  padding: 10px 10px;
}

.item_showcase p {
  font-size: 12px;
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

.dragging p {
  color: transparent;
  opacity: 1;
}

.dragging {
  display: none;
}

.hotkey p {
  display: none;
}

</style>
