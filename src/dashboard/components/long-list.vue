<template>
  <parent>
    <div>
      <ul>
        <li
          v-for="(item, index) in Array(100).fill('test')"
          :key="index"
        >
          {{ item }}-{{ index }}
        </li>
      </ul>
    </div>
  </parent>
</template>

<script>
  
import parent from './component.vue';

export default {
  name: 'List',
  components: {
    parent
  },
  extends: parent,
  data () {
    return {
      time: new Date(),
      i: 0
    }
  },
  defaults: {
    height: 2
  }
}
</script>
