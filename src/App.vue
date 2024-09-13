<template>
  <div id="app">
    <div class="first">
      <div class="first-blocks">
        <div class="block selected-items">
          <div class="block-header"></div>

          <div class="selected-list">
            <div
              v-for="(item, index) in selectedUserItems"
              :key="index"
              class="item-box"
            >
              {{ item.name }}
            </div>
          </div>
          <div class="selected-count">
            selected: {{ selectedUserItems.length }} / 6
          </div>
        </div>

        <div class="block selected-item">
          <div class="block-header">SELECTED ITEM</div>
          <div class="selected-item-name">
            <p v-if="selectedItemOnChoice">{{ selectedItemOnChoice.name }}</p>
            <p v-else>Nothing selected</p>
          </div>
        </div>
      </div>
    </div>
    <div></div>

    <div class="container">
      <ItemList
        title="User items"
        :items="userItems"
        :selectedItems="selectedUserItems"
        @toggleItem="toggleUserItem"
      />

      <ItemList
        title="Items for select"
        :items="itemsOnChoice"
        :selectedItem="selectedItemOnChoice"
        @selectItem="selectItemOnChoice"
        single-selection
      />
    </div>
  </div>
</template>

<script>
import ItemList from "./components/ItemList.vue";

export default {
  name: "App",
  components: {
    ItemList,
  },
  data() {
    return {
      userItems: [
        { id: 1, name: "Shoes 1" },
        { id: 2, name: "Shoes 2" },
        { id: 3, name: "Shoes 3" },
        { id: 4, name: "Shoes 4" },
        { id: 5, name: "T-shirt 1" },
        { id: 6, name: "T-shirt 2" },
        { id: 7, name: "T-shirt 3" },
        { id: 8, name: "T-shirt 4" },
      ],
      itemsOnChoice: [
        { id: 11, name: "Jacket 1" },
        { id: 12, name: "Jacket 2" },
        { id: 13, name: "Jacket 3" },
        { id: 14, name: "Jacket 4" },
        { id: 15, name: "Hoodie 1" },
        { id: 16, name: "Hoodie 2" },
        { id: 17, name: "Hoodie 3" },
        { id: 18, name: "Hoodie 4" },
      ],
      selectedUserItems: [],
      selectedItemOnChoice: null,
    };
  },
  methods: {
    toggleUserItem(item) {
      const index = this.selectedUserItems.indexOf(item);
      if (index > -1) {
        this.selectedUserItems.splice(index, 1);
      } else if (this.selectedUserItems.length < 6) {
        this.selectedUserItems.push(item);
      }
    },
    selectItemOnChoice(item) {
      this.selectedItemOnChoice = item;
    },
  },
};
</script>

<style scoped>
/* Общий контейнер для верхних блоков */
.first {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

/* Верхние блоки */
.first-blocks {
  display: flex;
  justify-content: space-between;
  width: 1200px;
}

.block {
  border: 2px solid black;
  padding: 20px;
  min-height: 100px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 420px;
}

.block-header {
  font-weight: bold;
  margin-bottom: 10px;
}

.selected-items {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.selected-list {
  display: flex;
  justify-content: space-around;
  margin-bottom: 10px;
}

.item-box {
  flex: 1 1 25%;
  flex-wrap: wrap;
  grid-auto-rows: 1fr;
  border: 1px solid black;
  padding: 5px;
  height: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.selected-count {
  font-size: 18px;
  margin-top: 10px;
  text-align: center;
}

.selected-item-name {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 50px;
  width: 100px;
  border: 1px solid black;
}

/* Контейнер для нижних списков */
.container {
  display: flex;
  justify-content: space-around;
  margin: 20px auto;
  width: 600px;
}

.block {
  border: 2px solid black;
  padding: 10px;
  min-height: 300px;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  margin-bottom: 10px;
  cursor: pointer;
  border: 1px solid black;
  padding: 10px;
  text-align: center;
}
</style>
