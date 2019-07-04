<template>
  <div>
    <h1>Page</h1>
    <button @click="add('text-component')">AddTextComponent</button>
    <button @click="add('carousel-component')">AddCarouselComponent</button>
    <button @click="send()">Send</button>
    <form id="form">
      <component
        :is="item.component"
        :key="item.id"
        :pushable_id="item.id"
        :pushable_name="item.pre_name"
        @remove="del"
        v-for="item in items"
      ></component>
    </form>
  </div>
</template>

<script>
import textComponent from "@/components/Text";
import carouselComponent from "@/components/Carousel";
import axios from "axios";

export default {
  name: "page",
  data() {
    return {
      items: [],
      id: 1
    };
  },
  components: {
    "text-component": textComponent,
    "carousel-component": carouselComponent
  },
  methods: {
    add: function(component) {
      this.items.push({
        id: this.id,
        pre_name: this.pre_name,
        component: component
      });

      this.id++;
    },
    del: function(id) {
      let index = this.items.findIndex(f => f.id === id);
      this.items.splice(index, 1);
    },
    send: function() {
      axios
        .post("https://96fadfc1.ngrok.io/test", this.form_data)
        .then(function(response) {
          console.log(response.data);
        })
        .catch(function(error) {
          console.log(error);
        });
    }
  },
  computed: {
    pre_name: function() {
      return "pushables[" + this.id + "]";
    },
    form_data: function() {
      let data = new FormData(document.getElementById("form"));
      return data;
    }
  }
};
</script>
