<template>
  <div class="show-more" :aria-label="text">
    <span v-if="escapeHtml">{{ short }}</span><span v-else v-html="short"></span><span v-if="isTruncated && escapeHtml">{{ more ? rest : ' ...' }}</span><span v-if="isTruncated && !escapeHtml" v-html="more ? rest : ' ...'"></span><!-- eslint-disable-line max-len -->
    &nbsp;<a @click="toggle" v-if="isTruncated" class="show-more__toggle">
      {{ $t(`elements.show-more.${more ? 'hide' : 'show'}`).replace(' ', '\xa0') }}
    </a>
  </div>
</template>

<script>
export default {
  name: 'ShowMore',
  data() {
    return {
      more: false,
    };
  },
  props: {
    text: {
      type: String,
      required: true,
    },
    length: {
      type: Number,
      default: 250,
    },
    escapeHtml: {
      type: Boolean,
      default: true,
    },
  },
  computed: {
    isTruncated() {
      return this.text.length > this.length;
    },
    short() {
      if (!this.isTruncated) {
        return this.text;
      }
      const truncated = this.text.substr(0, this.length);
      return truncated.substr(0, truncated.lastIndexOf(' '));
    },
    rest() {
      return this.text.substring(this.short.length);
    },
  },
  methods: {
    toggle() {
      this.more = !this.more;
    },
  },
};
</script>

<style lang="scss">
.show-more__toggle {
  font-weight: bold;
  cursor: pointer;
}
.show-more a {
  text-decoration: underline;
}
</style>
