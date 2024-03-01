<template>
  <div>
    <div class="title">
      <h1>Welcome</h1>
    </div>
    <nav class="navbar">
      <a href="/login">Log In</a>
    </nav>
  </div>
</template>

<style>
.title {
  display: flex;
  flex-direction: row-reverse;
  align-items: center;
  justify-content: center;
  height: 100vh; 
}

.navbar {
  position: absolute;
  top: 40px;
  right: 80px;
}

.navbar a {
  margin-right: 10px;
}

a {
  color: blue;
}
</style>
