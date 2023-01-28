<template>
  <div>
    <div class="d-flex flex-row mt-5">
      <div class="item-wrapper ms-5">
        <ToggleSelectInput
          label="Статус поставки"
          shortLabel="Статус"
          itemKey="description"
          tabIndex="1"
          :items="mockItems"
          v-model="firstValue"
        />
      </div>
      <div class="item-wrapper ms-5">
        <ToggleSelectInput
          label="Режим перемещения"
          shortLabel="Режим"
          itemKey="description"
          tabIndex="2"
          :items="mockItems2"
          v-model="secondValue"
        />
      </div>
    </div>
    <div class="d-flex flex-row mt-5">
      <div class="item-wrapper ms-5">
        В первом элементе выбранно {{ firstValue || "ничего" }}
      </div>
      <div class="item-wrapper ms-5">
        Во втором элементе выбранно {{ secondValue || "ничего" }}
      </div>
    </div>
  </div>
</template>

<script>
import ToggleSelectInput from "@/components/ToggleSelectInput.vue";

export default {
  name: "MainViewApp",
  components: {
    ToggleSelectInput,
  },
  data() {
    return {
      firstValue: null,
      secondValue: null,
      mockItems: [
        {
          code: 0,
          description: "Формируется",
        },
        {
          code: 10,
          description: "Товар прибыл",
        },
        {
          code: 20,
          description: "Товар прибыл (срочная поставка)",
        },
        {
          code: 30,
          description: "Оформление ДТ",
        },
        {
          code: 40,
          description: "ДТ выпущена",
        },
        {
          code: 50,
          description: "Поставка закрыта",
        },
      ],
      mockItems2: [
        {
          id: 1,
          description: "Импорт",
        },
        {
          id: 2,
          description: "Экспорт",
        },
      ],
    };
  },
  methods: {},
};
</script>
<style scoped>
.item-wrapper {
  width: 330px;
}
</style>
