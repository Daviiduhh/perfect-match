<script setup>
import { ref } from "vue";
import Tile from "./components/Tile.vue";

class Fruit {
  constructor(fruit) {
    this.id = fruit.id;
    (this.icon = fruit.icon),
      (this.color = fruit.color),
      (this.name = fruit.name),
      (this.visible = fruit.visible);
  }
}

const fruits = ref([
  {
    id: 0,
    icon: "/fruits/aguacate.svg",
    color: "#767df2",
    visible: false,
    name: "Aguacate",
  },
  {
    id: 1,
    icon: "/fruits/coco.svg",
    color: "#2f6da6",
    visible: false,
    name: "Coco",
  },
  {
    id: 2,
    icon: "/fruits/jitomate.svg",
    color: "#1adfff",
    visible: false,
    name: "Jitomate",
  },
  {
    id: 3,
    icon: "/fruits/naranja.svg",
    color: "#2f82ff",
    visible: false,
    name: "Naranja",
  },
  {
    id: 4,
    icon: "/fruits/granada.svg",
    color: "#34fefe",
    visible: false,
    name: "Granada",
  },
  {
    id: 5,
    icon: "/fruits/pera.svg",
    color: "#4e1fd3",
    visible: false,
    name: "Pera",
  },
  {
    id: 6,
    icon: "/fruits/maiz.svg",
    color: "#3038ff",
    visible: false,
    name: "Maiz",
  },
  {
    id: 7,
    icon: "/fruits/cebolla.svg",
    color: "#89e2bb",
    visible: false,
    name: "Cebolla",
  },
  {
    id: 8,
    icon: "/fruits/durazno.svg",
    color: "#81e0fe",
    visible: false,
    name: "Durazno",
  },
  {
    id: 9,
    icon: "/fruits/berenjena.svg",
    color: "#37a345",
    visible: false,
    name: "Berenjena",
  },
]);
const tiles = ref([]);
const selectedFruit = ref({});
const selectedFruits = ref([]);

const searchFruit = (fruits, fruitId) => {
  const found = fruits.find(
    (fruit) => fruit.id == fruitId
  );
  return found;
};

const selectFruit = () => {
  //Esta funcion solo se puede utilizar 10 veces
  do {
    const index = Math.floor(Math.random() * 10);
    selectedFruit.value = new Fruit(fruits.value[index]);
  } while (
    searchFruit(selectedFruits.value, selectedFruit.value.id) != undefined
  );
  selectedFruits.value.push(selectedFruit.value);
  console.log(selectedFruits.value);
};
</script>

<template>
  <main class="tiles">
    <span @click="selectFruit">funcion</span>
    <Tile
      v-for="fruit in fruits"
      :icon="fruit.icon"
      :color="fruit.color"
      :name="fruit.name"
      :visible="fruit.visible"
    />
  </main>
</template>

<style lang="scss" scoped>
.tiles {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(4, 1fr);
  justify-content: center;
  align-items: center;
  gap: 1rem;
}

.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
</style>
