<template>
  <!-- <div>
    {{dragArray}} -->
  <div class="expression-hole only-one"
    :class="{empty: dragArray.length === 0}"
		:data-type="type"
    v-dragula="dragArray" 
    bag="vue-blocks-expressions"
    @dragdrop="dragdrop($event)"
  >
    <component 
      v-for="item in dragArray" 
      :is="expressionComponent(item)" 
      :data="item" 
      :key="keyFor(item)"
      />
  </div>
<!-- </div> -->
</template>

<script>
// import { DragHandler } from 'vue2-dragula';
import BlockMixin from './BlockMixin';
import { expressions } from './Expression';

// class MyDragHandler extends DragHandler {

// }

// function createDragHandler({ctx, name, drake}) {
//   return new MyDragHandler({ ctx, name, drake })
// }

export default {
  name: 'expression-hole',
  mixins: [BlockMixin],
  props: ['value', 'type'],
  data() {
    let dragArray = [];
    if (this.value) {
      dragArray.push(this.value);
    }
    return {
      dragArray,
    };
  },
  watch: {
    dragArray: function(da) {
      if (da[0] !== this.value)
        this.$emit('input', da[0]);
    },
    value: function(val) {
      if (val !== this.dragArray[0]) {
        let dragArray = [];
        if (val) {
          dragArray.push(val);
        }
        this.dragArray = dragArray;
      }
    },
  },
  methods: {
    dragdrop(event) {
      this.$emit('input', event.model[0]);
    },
    expressionComponent(item) {
      if (!item) return null;

      return expressions[item._name];
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.expression-hole:empty, .expression-hole.dragging {
  min-height: 1em;
  min-width: 20px;
  box-shadow: inset 1px 1px 1px #444444;
}

.expression-hole > :nth-child(2) {
  display: none;
}

.expression-hole {
  position: relative;
  display: flex;
  align-self: stretch;
  align-items: stretch;
  background-color: white;
  padding: 1px;
  /*vertical-align: middle;*/
  border-radius: 2px;
  margin: 1px 0;
  overflow: hidden;
}

.block-text-inline > .expression-hole::before {
  border-left-color: #8888ff;
}

.block-right-hole > .expression-hole::before {
  border-left-color: #8888ff;
}

.block-text-inline.right-hole > .expression-hole:last-child::before {
  border-width: 9px;
  margin-top: -9px;
  margin-right: -17px;
}

.expression > .expression-hole::before {
  border-left-color: #ddddaa;
}

.expression-hole::before {
  right: 100%;
  top: 50%;
  border: solid transparent;
  content: " ";
  height: 0;
  width: 0;
  position: absolute;
  pointer-events: none;
  /*border-color: rgba(194, 225, 245, 0);*/
  border-width: 9px;
  margin-top: -9px;
  margin-right: -17.5px;
}
.expression-hole.empty::before, .expression-hole.dragging::before {
  filter: drop-shadow(1px 1px 1px #444444);
}

.block-text-inline.right-hole > .expression-hole:last-child {
  display: flex;
  /*position: absolute;*/
  margin-left: 5px;
  width: auto;
  height: auto;
  min-height: none;
  min-width: none;
  background: white;
  margin-top: 0;
  margin-bottom: 0;
  padding: 0;
  padding-left: 1px;
}


</style>
