<template>
  <div>
    <table>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
      </tr>
      <tr v-for="data in topContacts" :key="data.name">
        <td>
          <img
            :src="data.pictureUrl"
            :alt="`foto de ${data.name}`"
          />
        </td>
        <td>{{ data.name }}</td>
        <td>{{ data.popularity }}</td>
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
    };
  },
  computed: {
    topContacts() {
      return [...this.contacts].slice(0, 5);
    },
  },
};
</script>

<style></style>
