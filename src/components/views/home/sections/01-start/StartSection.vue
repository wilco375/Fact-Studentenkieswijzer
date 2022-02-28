<template>
  <PageSection
    tag="header"
    class="start-section"
    data-section="start"
    full
    role="banner"
    :aria-roledescription="$t('views.home.start.section.banner-aria')"
  >
    <!-- wrapping div needed for IE11 -->
    <div class="start-section__logo">
      <img width="300px" src="/logo.svg" alt="Fact logo">
    </div>
    <h1 class="start-section__heading">
      {{ $t('title') }}
    </h1>
    <p class="start-section__subtitle">{{ $t('subtitle') }}</p>
    <button v-if="activeLanguage.code == 'nl'" @click="activateLanguage('en')"
            class="start-section__button">
      Go to English version
    </button>
    <button v-else @click="activateLanguage('nl')" class="start-section__button">
      Ga naar Nederlandse versie
    </button>
  </PageSection>
</template>

<script>
import PageSection from '@/components/elements/PageSection.vue';

export default {
  name: 'StartSection',
  computed: {
    activeLanguage() {
      return this.$store.getters['languages/active'];
    },
  },
  components: {
    PageSection,
  },
  methods: {
    activateLanguage(code) {
      this.$store.commit('languages/activateLanguage', { code });
    },
  },
};
</script>

<style lang="scss">
.start-section {
  text-align: center;
}

.start-section__logo {
  display: inline-block;
  font-size: 4em;
  @media (min-width: 48em) {
    font-size: 6em;
  }
}

.start-section__heading {
  // `align-self` needed for IE11
  align-self: center;
  font-size: 1.5em;
  line-height: 1.25;
  text-align: center;
  max-width: 15em;
  margin: 1.5em auto 1em;
  @media (min-width: 38em) {
    font-size: 2em;
  }
  @media (min-width: 48em) {
    font-size: 3em;
  }
}

.start-section__subtitle {
  // `align-self` needed for IE11
  align-self: center;
  font-size: 0.875em;
  text-align: center;
  color: #999;
  @media (min-width: 48em) {
    font-size: 1.125em;
  }
  @media (min-width: 64em) {
    font-size: 1.25em;
  }
}

.start-section__button {
  display: inline-block;
  margin-top: 30px;
}
</style>
