<template>
    <div>
      <div class="mx-8 mt-5">
        <p>Users List</p>
        <table>
          <thead>
            <tr>
              <th>Name</th>
              <th>Email</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="t in users" :key="t.id">
              <td>{{ t.name }}</td>
              <td>{{ t.email }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
</template>
  
<script setup>
  definePageMeta ({
    layout: 'dashboard'
  });

  const { data:users } = await useFetch('http://127.0.0.1:8000/api/getUsers');
</script>
  
<style>
  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
  }

  th, td {
    padding: 8px;
    text-align: left;
  }

  th {
    background-color: lightskyblue;
  }
</style>