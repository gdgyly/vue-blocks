<template>
  <expression type="number">
    <span>{{data.value}}</span>
  </expression>
</template>

<script>
import {Expression} from 'src';

export default {
  name: 'number',
  props: ['data'],
  data() {
    return {
    };
  },
  components: {
    Expression,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

</style>
