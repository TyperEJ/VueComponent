<template>
  <div>
    <p>方塊</p>
    <input type="text" :name="text_name" v-model="text_input.value">
    <input type="hidden" :name="type_name" v-model="type_input.value">
    <button @click="del(bubble_id)">Delete</button>
  </div>
</template>

<script>
export default {
  props: ["bubble_id", "bubble_name"],
  data: function() {
    return {
      type_input: {
        value: "text"
      },
      text_input: {
        value: null
      }
    };
  },
  methods: {
    del(id) {
      this.$emit("remove", id);
    }
  },
  computed: {
    type_name: function() {
      return this.bubble_name + "[type]";
    },
    text_name: function() {
      return this.bubble_name + "[text]";
    }
  }
};
</script>
