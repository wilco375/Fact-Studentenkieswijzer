<template>
  <div class="match" role="figure">
    <div
      class="match__bar"
      role="img"
      :aria-label="$t('views.home.match.match.match-aria', {
        party: $t(`parties.${party.index}.name`),
        percentage: Math.round(percentage * 100),
      })"
    >
      <div class="match__progress" :style="`width:${percentage * 100}%`" />
      <span class="match__party-name">
        {{ $t(`parties.${party.index}.short`) }}
      </span>
      <span class="match__percentage">
        {{ $n(percentage, { style: 'percent' }) }}
      </span>
    </div>
    <p class="match__party-description" v-if="$t(`parties.${party.index}.description`) !== ''
    && $t(`parties.${party.index}.description`) !== '-'">
      <ShowMore :length="500" :text="$t(`parties.${party.index}.description`)"
                :escape-html="false" />
    </p>
  </div>
</template>

<script>
import ShowMore from '@/components/elements/ShowMore.vue';

export default {
  name: 'Match',
  components: {
    ShowMore,
  },
  props: {
    party: {
      type: Object,
      required: true,
    },
    percentage: {
      type: Number,
      required: true,
    },
  },
};
</script>

<style lang="scss">
.match {
  margin-bottom: 1em;
}

.match__bar {
  background-color: var(--theme-primary-dark-background); //bg-yellow-600
  border-radius: var(--border-radius);
  overflow: hidden;
  position: relative;
  margin-bottom: 1em;
}

.match__progress {
  background-color: #fff;
  position: absolute;
  top: 0;
  bottom: 0;
}

.match__party-name {
  font-weight: bold;
  color: #000;
  position: relative;
  display: block;
  padding: 1em;
}

.match__percentage {
  color: #000;
  position: absolute;
  display: block;
  padding: 1em;
  top: 0;
  right: 0;
  bottom: 0;
}

.match__party-description {
  margin-bottom: 2.5em;
  color: #000;
  font-size: 0.875em;
  @media (min-width: 40em) {
    font-size: 1em;
  }
}
</style>
