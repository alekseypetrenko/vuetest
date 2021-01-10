<template>
  <div class="container child">
    {{ person.name }}
    <input type="text" v-model="person.age" />
  </div>
</template>

<script>
export default {
  name: "Child",
  props: ["person"],
  watch: {
    person: {
      handler(newValue) {
        console.log(newValue.age);
      },
      deep: true,
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.container.child {
  max-width: 70%;
  margin: 1rem auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 1rem;
  border: 4px solid #ccc;
  border-radius: 12px;
}
</style>
