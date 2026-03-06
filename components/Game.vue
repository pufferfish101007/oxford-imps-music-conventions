<template>
  <details open>
    <summary>
      <span class="game-name">{{ props.name }}</span>
      &nbsp;
      <!-- {{ props.categories }} -->
      <span
        v-for="cat of props.category"
        :key="cat"
        class="cat"
        :class="'cat-' + cat"
      >
        {{ cat }}
      </span>
    </summary>

    <props.description />
  </details>
</template>

<script setup>
const props = defineProps(["name", "category", "description"]);
</script>

<style>
details {
  border: 1px solid #aaaaaa;
  border-radius: 4px;
  padding: 0.5em 0.5em 0;
  margin-bottom: 0.8em;
}

summary {
  font-weight: bold;
  margin: -0.5em -0.5em 0;
  padding: 0.5em;
}

details[open] {
  padding: 0.5em;
}

details[open] summary {
  border-bottom: 1px solid #aaaaaa;
  margin-bottom: 0.5em;
}

span.game-name {
  font-size: 1.2em;
  font-weight: bold;
}
</style>
