<template>
  <div>
    <h2>User List from API</h2>
    <button @click="fetchUsers">Load Users</button>
    <table v-if="users.length">
      <thead>
        <tr>
          <th>Name</th>
          <th>Email</th>
          <th>Gender</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.id">
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.gender }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  import axios from "axios";

  export default {
    data() {
      return {
        users: [],
      };
    },
    methods: {
      fetchUsers() {
        axios
          .get("https://gorest.co.in/public/v2/users")
          .then((response) => {
            this.users = response.data;
          })
          .catch((error) => {
            console.error(error);
          });
      },
    },
  };
</script>
