<template>
  <div id="app">
    <hr />
    <form>
      <input type="text" v-model="name" placeholder="Enter name..." />
      <input type="text" v-model="number" placeholder="Enter number..." />
      <button type="submit" v-on:click.prevent="addNewUser()">Add</button>
      <button v-on:click.prevent="saveStorage()">
        Save All
      </button>
    </form>
    <hr />
    <ol>
      <li v-for="(contact, index) in contacts" v-bind:key="index">
        {{ contact.name + " -- " + contact.number }}

        <button v-on:click="removeElement(index)">Remove</button>
        <hr />
      </li>
      <li v-for="(contact, index) in jsonParsed" v-bind:key="index">
        {{ contact.name + " -- " + contact.number }}
        <button v-on:click="removeElement(index)">Remove</button>
        <hr />
      </li>
    </ol>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      contacts: [],
      name: "",
      number: "",
      jsonParsed: [],
    };
  },
  mounted() {
    this.jsonParsed = JSON.parse(localStorage.getItem("data"));
    console.log(this.jsonParsed);
  },
  methods: {
    addNewUser() {
      let newUser = {
        name: this.name,
        number: this.number,
      };
      this.contacts.push(newUser);
      this.name = "";
      this.number = "";
    },
    removeElement(index) {
      if (this.contacts.length > 0) {
        this.contacts.splice(index, 1);
      } else if (this.jsonParsed.length > 0) {
        this.jsonParsed.splice(index, 1);
      }
    },
    saveStorage() {
      localStorage.setItem("data", JSON.stringify(this.contacts));
    },
  },
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
  border: solid 5px black;
  height: 700px;
  width: 500px;
  margin: 50px auto;
  background: rgba(28, 154, 204, 0.301);
}
li {
  font-size: 20px;
  text-align: left;
  margin-left: 15px;
}
</style>
