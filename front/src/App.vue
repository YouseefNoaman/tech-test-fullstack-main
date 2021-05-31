<template>
  <div
    v-bind:style="
      message == 'Welcome to Your Vue.js + TypeScript App'
        ? 'color:yellow;'
        : message == 'hello world'
        ? 'color:green;'
        : 'color: red;'
    "
  >
    <h1>{{ message }}</h1>
    <div v-bind:id="target_div" ref="target_div"></div>
    <h1></h1>
  </div>
</template>

<script>
var div = document.getElementById("target_div");

div.innerHTML += "hello world !";
</script>

<style>
.load {
  color: yellow;
}
.connected {
  color: green;
}
.failed {
  color: red;
}
</style>

<style>
#app {
  font-size: 18px;
  font-family: "Roboto", sans-serif;
  color: blue;
}
</style>



<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class App extends Vue {
  message = "Welcome to Your Vue.js + TypeScript App";
  messageFromLambda = "Wait..."
  async mounted() {
    const res = await fetch("http://localhost:3000/hello");
    if (res.ok) {
      const { message } = await res.json();
      this.message = message;
    } else {
      // get error message from body or default to response statusText
      console.error(`There has been an error, status = ${res.status} `);
    }
  }
}
</script>