<template>
  <div id="categories-filter">
    Search: <input type="text" v-model="searchText" />
    <br />
    <span
      >Categories:
      <label v-for="tag in allTags" :key="tag"
        ><input type="checkbox" v-model="tagFilters[tag]" /><span
          class="cat"
          :class="'cat-' + tag"
          >{{ tag }}</span
        ></label
      ></span
    >
  </div>
  <Game
    v-for="game in games"
    :key="game.name"
    :name="game.name"
    :category="game.category"
    :description="game.description"
    v-show="shouldShow(game)"
  />
  <div v-if="games.every(game => !shouldShow(game))">No results found.</div>
  <br/>
  <br/>
  <div id="bottom-text">Bottom text.</div>
</template>

<script setup>
import { reactive, ref } from "vue";
import Game from "./Game.vue";

const allTags = ["guessing", "longform", "music", "punning", "scene"];
const tagFilters = reactive(
  Object.fromEntries(allTags.map((tag) => [tag, true])),
);

const searchText = ref("");

const games_import = import.meta.glob("../games/*.jsx", {
  eager: true,
});
const games = Object.values(games_import).map((game) => ({
  name: game.name,
  category: Array.isArray(game.category) ? game.category : [game.category],
  description: game.description,
}));

function shouldShow(game) {
  let searched;
  if (searchText.value === "") searched = true;
  else {
    searched = game.name.toLowerCase().includes(searchText.value.toLowerCase());
  }
  return searched && game.category.some((tag) => tagFilters[tag]);
}
</script>

<style>
div#categories-filter {
  margin-bottom: 1em;
  position: sticky;
  padding: 0.5em;
  top: 0;
  background-color: white;
  border: 1px solid #aaaaaa;
  border-radius: 4px;
  & > span {
    display: inline-block;
    margin-top: 0.5em;
  }
}

div#bottom-text {
  position: absolute;
  bottom: 0.5em;
  padding-top: 1em;
}
</style>
