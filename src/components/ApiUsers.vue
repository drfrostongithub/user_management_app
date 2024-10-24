<template>
  <div class="api-table">
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

<style scoped>
  h2 {
    color: #333;
  }
  button {
    padding: 10px 15px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    margin-bottom: 15px;
  }
  button:hover {
    background-color: #0056b3;
  }
  .user-table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
  }
  .user-table,
  th,
  td {
    border: 1px solid #ccc;
  }
  th,
  td {
    padding: 10px;
    text-align: left;
  }
  th {
    background-color: #f2f2f2;
  }
  p {
    margin-top: 20px;
    font-style: italic;
    color: #777;
  }

  .api-table {
    display: flex;
    flex-direction: column;
    align-content: center;
    flex-wrap: wrap;
  }
</style>
