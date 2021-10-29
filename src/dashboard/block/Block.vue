<template>
  <article :style="{gridArea: name}">
    <OptionsButton
      v-if="options.length > 0"
      v-bind="{onClick: showOptions}"
    />
    <component
      :is="item.name"
      v-if="!optionsMode"
      :user-data="userData"
    />
    <OptionsCard
      v-if="optionsMode"
      v-bind="{options, onSubmit, userData}"
    />
  </article>
</template>

<script>
import OptionsButton from './OptionsButton';
import OptionsCard from './OptionsCard';
import components from '../components'

export default {
  name: 'Block',
  components: {
    ...components,
    OptionsButton,
    OptionsCard
  },
  props: {
    name: String,
    item: Object
  },
  data () {
    const userData = this.$store.state.components[this.item.name];
    return {
      optionsMode: false,
      userData: {
        weekOnly: false,
        inclusive: false,
        ...userData
      }
    }
  },
  computed: {
    options: function () {
      return this.item.options ? this.item.options() : []
    }
  },
  methods: {
    showOptions: function () {
      this.optionsMode = true
    },
    onSubmit: function (options) {
      if (options !== null) {
        this.$store.commit("updateComponent", {name: this.item.name, options});
        this.userData = Object.assign({}, this.userData, options);
      }
      this.optionsMode = false;
    }
  }
}
</script>

<style scoped>
article {
  overflow-y: auto;
  display: grid;
  align-items: center;
  justify-items: center;
  position: relative;

  padding: 1.5rem;
}
</style>
