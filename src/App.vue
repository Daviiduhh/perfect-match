<template>
  <header class="header">
    <h1 class="header__title">Perfect Match</h1>
    <h1 class="header__title">Level: {{ level }}</h1>
  </header>

  <section class="panel">
    <button v-show="gameState === 0" class="panel__start">Start Game!</button>
    <h2 v-show="gameState === 1" class="panel__memorise">Memorise the fruits!</h2>
    <Tile
      v-show="gameState === 2"
      class="panel__chosen"
      :icon="theChosenOne.icon"
      :color="theChosenOne.color"
      :name="theChosenOne.name"
      :visible="theChosenOne.visible"
    />
    <h2 class="panel__result" v-show="gameState === 3" v-text="resultMessage"></h2>
  </section>

  <main class="tiles">
    <Tile
      v-for="tile in tiles"
      :icon="tile.icon"
      :color="tile.color"
      :name="tile.name"
      :visible="tile.visible"
    />
  </main>
</template>

<script setup>
import { ref, onMounted } from "vue";
import Tile from "./components/Tile.vue";

class Fruit {
  constructor(fruit) {
    (this.id = fruit.id),
      (this.icon = fruit.icon),
      (this.color = fruit.color),
      (this.name = fruit.name),
      (this.visible = fruit.visible);
  }
}

onMounted(() => {
  for (let index = 0; index < 3; index++) {
    selectedFruits.value.push(selectFruit(fruits));
  }
  startGame();
});

const theChosenOne = ref({});
const level = ref(1);
const counter = ref(0);
const gameState = ref(0)
const intervalId = ref("");

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

const startGame = () => {
  setTiles();
  setTheChosenOne();
  startCounter(7);
};

const startCounter = (start) => {
  counter.value = start;
  intervalId.value = setInterval(() => {
    if (counter.value === 0) {
      clearInterval(intervalId.value);
    } else {
      counter.value--;
    }
  }, 1000);
};

const randomNumber = (max) => {
  return Math.floor(Math.random() * (max - 0) + 0);
};

const levelUp = () => {
  level.value++;
  selectedFruits.value.push(selectFruit(fruits));
  setTiles();
};

const setTheChosenOne = () => {
  const index = randomNumber(selectedFruits.value.length);
  theChosenOne.value = new Fruit(selectedFruits.value[index]);
};

const setTiles = () => {
  tiles.value = [];
  console.log(selectedFruits.value);
  for (let index = 0; index < 12; index++) {
    const index = randomNumber(selectedFruits.value.length);
    selectedFruit.value = new Fruit(selectedFruits.value[index]);
    tiles.value.push(selectedFruit.value);
  }
  console.log(tiles.value);
};

const searchFruit = (fruits, fruitId) => {
  const found = fruits.find((fruit) => fruit.id == fruitId);
  return found;
};

const selectFruit = (array) => {
  //Esta funcion solo se puede utilizar la longitud del array veces
  do {
    const index = randomNumber(array.value.length);
    selectedFruit.value = new Fruit(array.value[index]);
  } while (
    searchFruit(selectedFruits.value, selectedFruit.value.id) != undefined
  );

  return selectedFruit.value;
};
</script>

<style lang="scss" scoped>
.header {
  display: flex;
  justify-content: space-between;

  &__title {
    filter: drop-shadow(0 0 2em #fff);
  }
}

.panel {
  display: flex;
  justify-content: center;
}

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
