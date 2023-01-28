<template>
  <div class="position-relative">
    <div
      class="border border-success px-1 main-wrapper"
      @click="toggle"
      :tabindex="tabIndex"
      @focus="focused"
    >
      <div class="fw-weight-bold fs-6 text-start">{{ label }}</div>
      <p class="text-start selected-text fs-5 mb-0">
        {{ selectedItemText }}
      </p>
    </div>
    <div
      class="vw-100 vh-100 position-fixed top-0 left-0"
      v-show="isToggle"
      @click="close"
    ></div>
    <div
      class="border border-secondary overflow-auto item-list position-absolute"
      v-show="isToggle"
    >
      <div class="d-flex flex-row border-bottom border-2">
        <div class="fw-weight-bold text-start px-1">
          {{ shortLabel }}
        </div>
        <div @click="close" class="ms-auto me-3 fw-bold close-cross">
          &#10006;
        </div>
      </div>

      <div
        v-for="item in items"
        :key="item.code"
        @click="itemSelected(item)"
        class="text-start p-1 border-bottom select-item"
      >
        {{ item.description }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ToggleSelectInput",
  props: {
    label: {
      type: String,
      default: "Выберите пункт",
    },
    shortLabel: {
      type: String,
      default: "Выберите",
    },
    tabIndex: {
      type: Number,
      default: 1,
    },
    items: {
      type: Array,
      default: () => [],
    },
    itemKey: {
      type: String,
      default: "description",
    },
    value: {
      type: Object,
      default: () => {},
    },
  },
  data() {
    return {
      selectItem: null,
      isToggle: false,
    };
  },
  computed: {
    selectedItemText() {
      return (this.selectItem && this.selectItem[this.itemKey]) || "Не выбрано";
    },
  },
  mounted() {
    this.selectItem = { ...this.value };
  },
  methods: {
    toggle() {
      this.isToggle = !this.isToggle;
    },
    itemSelected(item) {
      this.selectItem = item;
      this.$emit("input", item);
      this.close();
    },
    close() {
      this.isToggle = false;
    },
    focused() {
      this.isToggle = true;
    },
  },
};
</script>
<style scoped>
.item-list {
  position: relative;
  z-index: 10;
  width: 100%;
  background-color: #fff;
  max-height: 180px;
}
.select-item:hover {
  background-color: #c8c8c8;
}
.main-wrapper:focus-visible {
  outline: 2px solid green;
}
.selected-text,
.close-cross,
.select-item {
  cursor: pointer;
}
/deep/ .fw-weight-bold {
  font-weight: bold;
}
</style>
