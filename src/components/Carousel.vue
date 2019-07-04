<template>
  <div>
    <p>輪播</p>
    <button type="button" @click="add('bubble-component')">AddBubbleComponent</button>
    <input type="hidden" :name="type_name" v-model="type_input.value">
    <component
      :is="item.component"
      :key="item.bubble_id"
      :bubble_id="item.bubble_id"
      :bubble_name="item.bubble_pre_name"
      v-for="item in bubbles"
      @remove="delBubble"
    ></component>
    <button @click="delRow(pushable_id)">Delete</button>
  </div>
</template>

<script>
import bubbleComponent from "./Bubble";

export default {
  data() {
    return {
      type_input: {
        value: "carousel"
      },
      bubbles: [],
      bubble_id: 1
    };
  },
  props: ["pushable_id", "pushable_name"],
  components: {
    "bubble-component": bubbleComponent
  },
  methods: {
    add(component) {
      this.bubbles.push({
        bubble_id: this.bubble_id,
        bubble_pre_name: this.pre_name,
        component: component
      });

      this.bubble_id++;
    },
    delBubble: function(id) {
      let index = this.bubbles.findIndex(f => f.bubble_id === id);
      this.bubbles.splice(index, 1);
    },
    delRow(id) {
      this.$emit("remove", id);
    }
  },
  computed: {
    type_name: function() {
      return this.pushable_name + "[type]";
    },
    pre_name: function() {
      return this.pushable_name + "[bubbles][" + this.bubble_id + "]";
    }
  }
};
</script>
