<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
        <router-link :to="{name: 'products'}"
        class="nav-link">
      <h1 class="navbar-brand font-bold text-primary">ToNote</h1>
        </router-link>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        </ul>
        <ul class="navbar-nav">
          <li class="nav-item dropdown">
            <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
              <i class="bi bi-person-circle"></i> {{ user.user.username }}
            </a>
            <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
              <li><a class="dropdown-item" href="#">My orders</a></li>
              <li><hr class="dropdown-divider"></li>
              <li><button class="dropdown-item" @click="logout()">Logout</button></li>
            </ul>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
import { useRouter } from 'vue-router';
import axiosClient from "../../axios";
import Auth from "../Auth";


export default({
setup() {
    const router = useRouter();

    const user = Auth.getAuthUser();

    function logout() {
        axiosClient.post("/logout")
        .then(() => {
            Auth.clearAuthUser();
            router.push({path: "/login"});
        });
    };
        return {
            logout,
            user,
        }
},
})
</script>

<style>

</style>

