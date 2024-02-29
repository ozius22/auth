<template>
  <div>
    <div class="center">
      <button @click="goTo('/login')">Log In</button>
      <button class="but2" @click="goTo('/register')">Sign Up</button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    goTo(path) {
      this.$router.push(path);
    }
  }
}
</script>

<style>
.center {
  display: flex;
  flex-direction: row-reverse;
  align-items: center;
  justify-content: center;
  height: 100vh; 
}

.but2 {
  margin-right: 10px;
}
</style>