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
            <tr v-for="t in data.users" :key="t.id">
              <td>{{ t.name }}</td>
              <td>{{ t.email }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </template>
  
  <script>
  definePageMeta ({
    layout: 'dashboard'
  })

  export default {
    async setup() {
      const data = ref(null);

      onMounted(() => {
        checkLogged();
      });

      async function checkLogged() {
        if (!localStorage.getItem('_token')) {
            console.log('no token');
        }
      }
      try {
        const { data } = await useFetch('http://127.0.0.1:8000/api/getUsers/'); 
  
        return { data };
      } catch (error) {
        console.error('Error fetching users:', error);
      }
    },
};
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