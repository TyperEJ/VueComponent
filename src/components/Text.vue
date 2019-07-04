<template>
  <div>
    <p>文字訊息</p>
    <input type="text" :name="text_name" v-model="text_input.value">
    <input type="hidden" :name="type_name" v-model="type_input.value">
    <button @click="delRow(pushable_id)">Delete</button>
  </div>
</template>

<script>
export default {
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
  props: ["pushable_id", "pushable_name"],
  methods: {
    delRow(id) {
      this.$emit("remove", id);
    }
  },
  computed: {
    type_name: function() {
      return this.pushable_name + "[type]";
    },
    text_name: function() {
      return this.pushable_name + "[text]";
    }
  }
};
</script>
