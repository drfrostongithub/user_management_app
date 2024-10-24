<template>
  <div>
    <h1>User Management App</h1>

    <div>
      <button @click="currentPage = 'userTable'">User Table</button>
      <button @click="currentPage = 'apiUsers'">API Users</button>
      <button @click="currentPage = 'registerUser'">Register User</button>
    </div>

    <div v-if="currentPage === 'userTable'">
      <UserTable />
    </div>

    <div v-if="currentPage === 'apiUsers'">
      <ApiUsers />
    </div>

    <div v-if="currentPage === 'registerUser'">
      <RegisterUser />
    </div>
  </div>
</template>

<script>
  import UserTable from "./components/UserTable.vue";
  import ApiUsers from "./components/ApiUsers.vue";
  import RegisterUser from "./components/RegisterUser.vue";

  export default {
    data() {
      return {
        currentPage: "userTable",
      };
    },
    components: {
      UserTable,
      ApiUsers,
      RegisterUser,
    },
  };
</script>

<style scoped>
  h1 {
    text-align: center;
  }
  div {
    text-align: center;
  }
  button {
    margin: 10px;
    padding: 10px;
    background-color: #007bff;
    color: white;
    border: none;
    cursor: pointer;
  }
  button:hover {
    background-color: #0056b3;
  }
</style>
