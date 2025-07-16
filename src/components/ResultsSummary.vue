<script setup>
import SingularScore from './SingularScore.vue';

defineProps({
  data: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <div class="results-summary__container">
    <div class="results-summary">
      <div class="results-summary__overall">
        <div class="results-summary__overall-inner flow">
          <h2 class="results-summary__overall-heading text-preset4">
            Your Result
          </h2>
          <div class="results-summary__overall-score-container">
            <span class="results-summary__overall-score text-preset1">{{
              data.score
            }}</span>
            <span class="results-summary__overall-out-of text-preset5-bold"
              >of 100</span
            >
          </div>
          <div class="results-summary__overall-description">
            <p class="results-summary__overall-category text-preset3">
              {{ data.category }}
            </p>
            <p class="results-summary__overall-percentile text-preset5-medium">
              You scored higher than {{ data.percentile }}% of the people who
              have taken these tests.
            </p>
          </div>
        </div>
      </div>

      <div class="results-summary__breakdown">
        <div class="results-summary__breakdown-inner flow">
          <h2 class="results-summary__breakdown-heading text-preset4">
            Summary
          </h2>
          <ol>
            <SingularScore
              v-for="item in data.subscores"
              :score="item"
            ></SingularScore>
          </ol>
          <button
            class="results-summary__continue-button text-preset5-bold"
            type="button"
          >
            Continue
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.results-summary__container {
  container-type: inline-size;
}

.results-summary {
  color: hsl(var(--color-text-primary));
  background: hsl(var(--color-background-primary));

  display: grid;
  grid-template-areas: 'overall' 'breakdown';
}

.results-summary__overall {
  grid-area: overall;
  color: hsl(var(--color-text-secondary));
  background: var(--color-background-secondary);
  border-radius: 0 0 var(--border-radius-outer) var(--border-radius-outer);

  display: grid;
  place-items: center;
  padding-block: 32px;
}

.results-summary__overall-inner {
  max-inline-size: var(--inline-size-overall);
  text-align: center;
  --flow-space: var(--flow-space-overall);
}

.results-summary__overall-score-container {
  padding: 1rem;
  display: grid;
  background: var(--gradient1);
  border-radius: 50%;
  aspect-ratio: 1 / 1;
  align-content: center;
  justify-items: center;
  max-inline-size: var(--inline-size-overall-score);
  margin-inline: auto;
}

.results-summary__overall-score,
.results-summary__overall-category {
  color: hsl(var(--color-white));
}

.results-summary__overall-out-of {
  color: hsl(var(--color-navy-200) / 51.68%);
}

.results-summary__overall-percentile {
  margin-block-start: var(--flow-space-description);
}

.results-summary__breakdown {
  grid-area: breakdown;
  display: grid;
  align-items: center;
  padding-block: var(--padding-block-breakdown);
  padding-inline: var(--padding-inline-breakdown);
  --flow-space: var(--flow-space-breakdown);
}

.results-summary__breakdown ol {
  padding: 0;
  display: grid;
  gap: var(--space-200);
}

.results-summary__continue-button {
  border-radius: var(--br-800);
  border: none;
  cursor: pointer;
  color: hsl(var(--color-white));
  background-color: hsl(var(--color-navy-950));
  font-size: var(--fs-500);
  padding: 0;
  inline-size: 100%;
  block-size: 56px;
}

.results-summary__continue-button:hover,
.results-summary__continue-button:focus-visible {
  background: var(--gradient2);
}

.results-summary__continue-button:focus-visible {
  outline: 2px dashed hsl(241 81% 54%);
  outline-offset: 2px;
}

/* Move to 2 column format */

@container (min-width: 44rem) {
  .results-summary {
    border-radius: var(--border-radius-outer);
    box-shadow: var(--box-shadow1);

    grid-template-areas: 'overall breakdown';
    /* TODO: account for the difference in inline size of the two columns in the tablet view */
    /* grid-template-columns: minmax(338px, 368px) 1fr; */
    grid-template-columns: repeat(2, 1fr);
  }

  .results-summary__overall {
    border-radius: var(--border-radius-outer);
    padding-block: 45px;
  }

  .results-summary__breakdown {
    --flow-space: var(--space-400);
  }
}

@media (min-width: 44rem) {
  .results-summary {
    inline-size: min(
      100% - 2 * var(--inline-size-gutter),
      var(--inline-size-max)
    );
    margin-inline: auto;
  }
}
</style>
