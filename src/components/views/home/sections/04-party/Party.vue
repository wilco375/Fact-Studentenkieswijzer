<template>
  <div
    :class="{
      party: true,
      'party--selected': selected,
      'party--logo': showLogo && logo,
    }"
    role="listitem"
  >
    <button
      :for="`party-${index}-checkbox`"
      class="party__button"
      :aria-label="$t('views.home.party.party.party-aria', { party: $t(`parties.${index}.name`) })"
      role="checkbox"
      tabindex="0"
      :aria-checked="selected"
      @click="selected = !selected"
    >
      <div v-if="showLogo && logo" class="party__logo" aria-hidden="true">
        <img :src="logo" :alt="$t(`parties.${index}.name`)" />
      </div>
      <div class="party__caption" aria-hidden="true">
        <Icon
          :name="selected ? 'check' : 'circle'"
          class="party__icon"
        />
        <div class="party__details" aria-hidden="true">
          <span class="party__short">{{ $t(`parties.${index}.short`) }}</span>
          <span class="party__name">{{ $t(`parties.${index}.name`) }}</span>
        </div>
      </div>
    </button>
  </div>
</template>

<script>
export default {
  name: 'Party',
  props: {
    index: {
      type: Number,
      required: true,
    },
    showLogo: {
      type: Boolean,
      default: false,
    },
    logo: {
      type: String,
      default: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABAQMAAAAl21bKAAAAA1BMVEXe4+j77++FAAAACklEQVR4AWNhAAAACgAF3HyfDQAAAABJRU5ErkJggg==',
    },
  },
  computed: {
    selected: {
      get() {
        return this.$store.getters['parties/parties'][this.index].selected;
      },
      set(value) {
        this.$store.commit('parties/setSelected', { index: this.index, value });
      },
    },
  },
};
</script>

<style lang="scss">
.party__button {
  width: 100%;
  padding: 1em;
  display: block;
  margin-bottom: 1em;
  align-items: center;
  justify-content: flex-start;
  border-radius: var(--border-radius);
  border: 1px solid var(--theme-neutral-border);
  cursor: pointer;
  transition-property: border-color, box-shadow, background-color;
  transition-duration: 0.2s;
  transition-timing-function: ease-out;
  box-shadow: var(--shadow-normal);
  border: 1px solid var(--theme-neutral-border);
  background-color: var(--theme-neutral-background);
  color: var(--theme-neutral-text);
  font-size: 1em;
  &:hover {
    box-shadow: var(--shadow-hover);
  }
  &:focus {
    outline: 0;
    box-shadow: var(--shadow-focus);
  }
  @media (min-width: 50em) {
    font-size: 1.25em;
  }
}

.party--selected .party__button {
  border: 1px solid #718096;
  background-color: #A0AEC0;
  color: var(--theme-primary-text);
}

.party__icon {
  color: #fff;
  margin-right: 1em;
  flex: 0 1 auto;
}

.party__logo {
  img {
    width: 60px;
    height: 60px;
    object-fit: contain;
  }
}

.party__caption {
  display: flex;
  align-items: center;
}

.party__details {
  flex: 1 1 auto;
  display: flex;
  align-items: center;
}

.party__short {
  flex: 0 1 auto;
  font-weight: bold;
  margin-right: 2em;
}

.party__name {
  flex: 1 1 auto;
  text-align: right;
  word-wrap: anywhere;
  hyphens: auto;
  font-size: 1em;
  @media (min-width: 48em) {
    font-size: 0.75em
  }
}

.party--logo {
  height: 100%;

  .party__button {
    display: flex;
    align-items: center;
    flex-direction: row-reverse;
    padding: 0.5em 1em;
  }

  .party__caption {
    flex: 1 1 auto;
    display: flex;
    align-items: center;
    text-align: left;
    order: 1;
    width: 100%;
  }

  .party__details {
    display: block;
    flex: 1 1 auto;
    margin-right: 0.75em;
    span {
      display: block;
    }
    @media (min-width: 48em) {
      margin-right: 0;
    }
  }

  .party__short {
    margin-right: 0;
  }

  .party__name {
    text-align: left;
  }
}
</style>
