<template>
  <div class="block">
    <h3>{{ title }}</h3>
    <ul>
      <li
        v-for="item in items"
        :key="item.id"
        :class="{ selected: isSelected(item) }"
        @click="handleClick(item)"
      >
        {{ item.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "ItemList",
  props: {
    title: {
      type: String,
      required: true,
    },
    items: {
      type: Array,
      required: true,
    },
    selectedItems: {
      type: Array,
      default: () => [],
    },
    selectedItem: {
      type: Object,
      default: null,
    },
    singleSelection: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleClick(item) {
      if (this.singleSelection) {
        this.$emit("selectItem", item);
      } else {
        this.$emit("toggleItem", item);
      }
    },
    isSelected(item) {
      if (this.singleSelection) {
        return this.selectedItem && this.selectedItem.id === item.id;
      }
      return this.selectedItems.includes(item);
    },
  },
};
</script>

<style scoped>
.item {
  cursor: pointer;
  margin: 5px 0;
  padding: 5px;
  border: 1px solid black;
}
.selected {
  background-color: lightgreen;
}
</style>
