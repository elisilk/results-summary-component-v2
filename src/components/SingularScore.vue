<script setup>
const props = defineProps({
  score: {
    type: Object,
    required: true,
  },
});

function getImageUrl(filename) {
  return new URL(`../assets/images/${filename}`, import.meta.url).href;
}
</script>

<template>
  <li
    class="singular-score"
    :class="['singular-score--' + score.category.toLowerCase()]"
  >
    <div class="singular-score__label">
      <img
        class="singular-score__label-icon"
        :src="getImageUrl(score.icon)"
        width="20"
        height="20"
        alt=""
      />
      <span class="singular-score__label-text text-preset5-medium">{{
        score.category
      }}</span>
    </div>
    <div class="singular-score__value text-preset5-bold">
      <span class="singular-score__value-score">{{ score.score }}</span>
      <span class="singular-score__value-out-of">/ 100</span>
    </div>
  </li>
</template>

<style scoped>
.singular-score {
  --_color-primary: var(--color-primary, var(--color-text-primary));
  --_color-secondary: var(--color-secondary, var(--color-text-secondary));

  list-style: none;
  display: flex;
  align-items: center;
  justify-content: space-between;

  border-radius: var(--border-radius-inner);
  background-color: hsl(var(--_color-secondary));
  block-size: 56px;
  padding-inline: var(--space-200);
}

.singular-score__label {
  color: hsl(var(--_color-primary));
  display: flex;
  gap: var(--space-200);
}

.singular-score__value {
  display: flex;
  gap: var(--space-100);
}

.singular-score__value-out-of {
  color: hsl(var(--color-text-primary) / 50%);
}

.singular-score--reaction {
  --color-primary: var(--color-red-400);
  --color-secondary: var(--color-red-50);
}

.singular-score--memory {
  --color-primary: var(--color-yellow-400);
  --color-secondary: var(--color-yellow-50);
}

.singular-score--verbal {
  --color-primary: var(--color-green-500);
  --color-secondary: var(--color-green-50);
}

.singular-score--visual {
  --color-primary: var(--color-blue-800);
  --color-secondary: var(--color-blue-50);
}
</style>
