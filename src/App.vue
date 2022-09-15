<template>
  <div>
    <h1>List of Contacts</h1>
    <div class="sortbuttons">
      <button @click="addRandomContact">Add Random Contact</button>
    <button @click ="sortByName">Sort by name</button>
    <button @click ="sortByPopularity">Sort by popularity</button>
    </div>
    
    <table>
      <thead>
          <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won Oscar</th>
        <th>Won Emmy</th>
        <th>Actions</th>
      </thead>
      <tr v-for="(data, index) in topContacts" :key="data.name">
        <td class="picture">
          <img :src="data.pictureUrl" :alt="`foto de ${data.name}`" />
        </td>
        <td>{{ data.name }}</td>
        <td>{{ data.popularity }}</td>
        <td v-if="data.wonOscar === true">&#127942</td>
        <td v-else-if="data.wonOscar === false">Oh no &#128533</td>
        <td v-if="data.wonEmmy === true">⭐</td>
        <td v-else-if="data.wonEmmy === false">Oh no &#128533</td>
        <td><button @click="deleteContact (index)">Delete</button></td>
      </tr>
    </table>
  </div>
</template>

<script>
import json from "./contacts.json";
export default {
  data() {
    return {
      contacts: json,
      topContacts: json.slice(20, 25),
    };
  },
  methods: {
    addRandomContact() {
      const filteredContacts = this.contacts.filter(
        (contact) => !this.topContacts.includes(contact)
      );
      const randomContact =
        filteredContacts[Math.floor(filteredContacts.length * Math.random())];
      this.topContacts.push(randomContact);
      console.log(randomContact);
    },
    sortByName() {
      this.topContacts.sort((a, b) => a.name.localeCompare(b.name));
    },
    sortByPopularity() {
      this.topContacts.sort((a, b) => b.popularity - a.popularity);
    },
    deleteContact(index) {
      this.topContacts.splice(index, 1);
    },
  },
};
</script>

<style>

body {
  font-family: Helvetica;
  margin-top: 5%;
  margin-left: 5%;
  margin-right: 5%;
}
.sortbuttons {
  display: flex;
  justify-content: space-around;
  margin-bottom: 3%;
}

h1 {
  display: flex;
  justify-content: center;
}

table {
  width: 100%;
  text-align: center;
}

thead {
  background: #ececec;
}

.picture {
  width: 20%;
}

img {
  width: 100%;
  margin-top: 2%;
  margin-bottom: 0%;
}

</style>