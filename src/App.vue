<script setup>
import { useUserStore } from './stores/users';
import { ref } from 'vue'
import UserForm from './UserForm.vue'

const user_store = useUserStore()

const sort = ref(false)

const DeleteUser = id => {
  user_store.delete(id)
  alert("User Deleted with id: " + id)
}
</script>

<template>
  <main>
   <UserForm/>
    <h2>Users</h2>

    <label><span>Sort by name </span><input type="checkbox" v-model="sort"></label>

    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Full name</th>
          <th>Email</th>
          <th>Gender</th>
          <th>Age group</th>
          <th>Comment</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody class="users" v-if="!sort">
        <tr v-for="user in user_store.users" class="user">
          <td>{{ user.id }}</td>
          <td>{{ user.name }} {{ user.lname }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.gender }}</td>
          <td>{{ user.age }}</td>
          <td>{{ user.message }}</td>
          <td><button @click="DeleteUser(user.id)">DELETE</button></td>
        </tr>
      </tbody>
      <tbody class="users" v-else>
        <tr v-for="user in user_store.usersByName" class="user">
          <td>{{ user.id }}</td>
          <td>{{ user.name }} {{ user.lname }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.gender }}</td>
          <td>{{ user.age }}</td>
          <td>{{ user.message }}</td>
          <td><button @click="DeleteUser(user.id)">DELETE</button></td>
        </tr>
      </tbody>
    </table>

  </main>
</template>

<style scoped>
body {
  background: #ececec;
}

main {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

button {
  background: #d8e5f8;
  border: 2px solid #385170;
  border-radius: 20px;
  padding: 5px 10px;
  color: #385170;
  transition: 0.5s;
}


button:hover {
  background: #385170;
  border: 2px solid #d8e5f8;
  color: #d8e5f8;
}

h1,
h2 {
  text-align: center;
  color: #385170;
}

table {
  width: 100%;
  border: 2px solid #385170;
  background: #fff;
  margin-bottom: 20px;
  margin-top: 20px;
}

table th {
  background-color: #d8e5f8;
  border: 1px solid #385170;
  font-size: 1.2rem;
  padding: 3px 6px;
  font-weight: normal;
  cursor: default;
}

table tr td {
  border: 1px solid #385170;
  padding: 5px 6px;
  font-size: 1rem;
}

table tr.alt td {
  background-color: #E2E2E2;
}

table tr:hover {
  background-color: #F0F0F0;
}
</style>
