<template>
  <div id="app">
    <hr />
    <form>
      <input type="text" v-model="name" placeholder="Enter name..." />
      <input type="text" v-model="number" placeholder="Enter number..." />
      <button type="submit" v-on:click.prevent="addNewUser()">Add</button>
    </form>
    <hr />
    <ol>
      <li v-for="(user, index) in users" v-bind:key="index">
        {{ user.name + " -- " + user.number }}
        <button v-on:click="saveStorage(user.name, user.number)">Save</button>
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
      users: [],
      name: "",
      number: "",
    };
  },
  methods: {
    addNewUser() {
      let newUser = {
        name: this.name,
        number: this.number,
      };
      this.users.push(newUser);
      this.name = "";
      this.number = "";
    },
    removeElement(index) {
      this.users.splice(index, 1);
    },
    saveStorage(a, b) {
      localStorage.setItem(a, b);
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
