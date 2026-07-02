<template>
  <nav class="navbar">
    <div class="logo">🎓 CGPA Management Portal</div>
    <div class="nav-links">
      <router-link to="/">Dashboard</router-link>
      <router-link to="/history">Calculation History</router-link>
    </div>
  </nav>
  <main class="app-content">
    <router-view />
  </main>
</template>

<style>
body {
  margin: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #f8f9fa;
  color: #2c3e50;
}

.navbar {
  background-color: #d35400; /* Rich Dark Orange / Saffron */
  padding: 15px 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

.logo {
  color: white;
  font-weight: 700;
  font-size: 22px;
}

.nav-links a {
  color: white;
  margin-left: 25px;
  text-decoration: none;
  font-weight: 500;
  font-size: 16px;
  padding-bottom: 5px;
  opacity: 0.8;
  transition: all 0.3s ease;
}

.nav-links a:hover {
  opacity: 1;
}

.nav-links a.router-link-exact-active {
  opacity: 1;
  border-bottom: 3px solid white;
}

.app-content {
  padding: 30px 20px;
}
</style>
