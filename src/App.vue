<template>
  <div id="app">
    <div class="container computedVSMethods">
      <h2>Computed VS Methods</h2>
      <button @click="count++">Click</button> <span> {{ count }}</span>
      <input type="text" v-model="name" />
      <p>From func: {{ fullNameFunction() }}</p>
      <p>Computed: {{ fullNameComputed }}</p>
    </div>

    <div class="container reactivity">
      <h2>Reactivity</h2>
      {{ son }}
      <button @click="addNewFieldVersion1">Click 1</button>
      <button @click="addNewFieldVersion2">Click 2</button>
      <button @click="addNewFieldVersion3">Click 3</button>
      <div v-if="sonWeight">
        {{ son.weight }}
        <input type="text" v-model="son.weight" />
      </div>
    </div>

    <div class="container">
      <Child :person="person" v-for="person in people" :key="person.id" />
    </div>
    <div id="container">
      <h2>getter setter</h2>
      <span>a = {{ a }}</span>
      <span>b = {{ b }}</span>

      <button @click="b++">Set b</button>
    </div>
  </div>
</template>

<script>
import Child from "./components/Child.vue";

export default {
  name: "App",
  components: {
    Child,
  },
  data() {
    return {
      son: {
        name: "Alex",
        age: 30,
      },
      count: 0,
      name: "",
      a: 0,
      sonWeight: false,
      people: [
        { id: 0, name: "Alex", age: 10 },
        { id: 1, name: "Ivan", age: 20 },
        { id: 2, name: "Ann", age: 30 },
      ],
    };
  },
  methods: {
    changeAge() {
      this.son.age += 1;
    },
    fullNameFunction() {
      console.log("I am full name function");
      if (this.name === "") {
        return "";
      }
      return this.name + " Petrenko";
    },
    addNewFieldVersion1() {
      this.son.weight = 90;
      // this.$set(this.son, "weight", 90);
      this.sonWeight = true;
    },
    addNewFieldVersion2() {
      this.son.weight = 100500;
      this.sonWeight = true;
    },
    addNewFieldVersion3() {
      this.son = { weight: 666 };
      this.sonWeight = true;
      console.log(this.son);
    },
  },
  computed: {
    fullNameComputed: {
      get() {
        console.log("I am full name computed property");
        if (this.name === "") {
          return "";
        }
        return this.name + " Petrenko";
      },
    },
    b: {
      get() {
        return this.a + 5;
      },
      set(val) {
        this.a = val + 1;
      },
    },
  },
  watch: {},
};
</script>
 
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.container {
  max-width: 70%;
  margin: 2rem auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 2rem;
  border: 4px solid #ccc;
  border-radius: 12px;
}

.computedVSMethods {
  background-color: #add8e6;
}

.reactivity {
  background-color: #d8e6ad;
}
</style>
