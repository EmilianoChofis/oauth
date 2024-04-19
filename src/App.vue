<script setup>
import {GoogleLogin} from "vue3-google-login";
</script>

<template>
  <div v-if="loggedIn">
    <button @click="logout">logout</button>
    <h2>name: {{user.name}}</h2>
    <h2>email: {{user.email}}</h2>
    <img :src="user.picture" alt="">
  </div>
  <GoogleLogin :callback="callback" prompt auto-login/>
</template>
<script>
import {decodeCredential, googleLogout} from "vue3-google-login";

export default {
  data() {
    return {
      loggedIn: false,
      user: null,
      callback: (response) => {
        console.log('login')
        this.loggedIn = true;
        console.log(response);
        this.user = decodeCredential(response.credential);
      },
      logout() {
        googleLogout();
        this.loggedIn = false;
        this.user = null;
      }
    }
  }
}
</script>


