<template>
  <header>
    <!-- Slot are like children in react components  -->
    <TextComp :msg="msg"> If slot is passed </TextComp>
    <div class="wrapper">
      <h1>{{ message }}</h1>
      <button @click="increment">Add</button>
      <p ref="o"></p>
    </div>

    <input type="text" v-model="text" />
  </header>
  <br />

  <p :class="title">Red text</p>
  <br />

  <h1 v-if="awesome">Vue is awesome</h1>
  <h1 v-else>Oh no</h1>
  <br />
  <button @click="toggle">Toggle</button> <br />
  <ToDo /> <br />
  <br />
  <AsncyToDo />

  <TextComp @response="(msg) => (childMsg = msg)" :msg="childMsg" />
</template>

<script>
import ToDo from "./components/ToDo.vue";
import AsncyToDo from "./components/AsncyToDo.vue";
import TextComp from "./components/TextComp.vue";

export default {
  components: {
    ToDo,
    AsncyToDo,
    TextComp,
  },
  data() {
    return {
      message: "Hello Shanas!",
      counter: 0,
      title: "title",
      text: "",
      awesome: true,
      msg: "Vue Js",
      childMsg: "",
    };
  },
  // watchers func names should be the same as the state variables it watches
  watch: {
    counter(newCount) {
      this.$refs.o.textContent = `New count is ${newCount}`;
    },
  },
  methods: {
    increment() {
      this.counter++;
    },
    toggle() {
      this.awesome = !this.awesome;
    },
  },
};
</script>

<style>
.title {
  color: red;
}
</style>
