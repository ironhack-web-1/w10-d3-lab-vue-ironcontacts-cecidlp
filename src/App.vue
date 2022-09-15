<template>
  <div>
    <button @click="addRandomContact">Add Random Contact</button>
    <button @click ="sortByName">Sort by name</button>
    <button @click ="sortByPopularity">Sort by popularity</button>
    <table>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won Oscar</th>
        <th>Won Emmy</th>
        <th>Actions</th>
      </tr>
      <tr v-for="(data, index) in topContacts" :key="data.name">
        <td>
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
      topContacts : json.slice(20, 25)
    };
  },
  methods: {
    addRandomContact() {
        const filteredContacts = this.contacts.filter(contact => !this.topContacts.includes(contact))
        const randomContact = filteredContacts[Math.floor(filteredContacts.length * Math.random())]
        this.topContacts.push(randomContact)
        console.log(randomContact)
    },
    sortByName(){
    this.topContacts.sort((a, b) => a.name.localeCompare (b.name) );
  },
  sortByPopularity() {
    this.topContacts.sort((a, b)=> b.popularity - a.popularity); 
  },
  deleteContact(index) {
    this.topContacts.splice(index, 1);
  }
},
};
</script>

<style></style>
