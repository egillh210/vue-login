<template>
  <div id="logincomponent">
    <img class="logo" src="../assets/logo.png" alt="logo" />
    <h1>Chatbot Tool</h1>
    <div>
      <div class="title">
        Username: <br>
      </div>
      <i class="fas fa-user fa-2x"></i>
      <input 
      v-model="api.body.username" 
      type="text" 
      placeholder="filippo.peddrazini@gavagai.com"
      onfocus="this.placeholder = ''"
      onblur="this.placeholder='filippo.peddrazini@gavagai.com'"
      >
      <br>
      <div class="title">Password: <br></div>
      <i class="fas fa-lock fa-2x"></i>
      <input 
      v-model="api.body.password" 
      type="password" 
      placeholder="***************"
      onfocus="this.placeholder=''"
      onblur="this.placeholder='***************'"
      >
    </div>
    <div class="loader_error">
      <div v-if="loading" class="lds-ring"><div></div><div></div><div></div><div></div></div>
      <h2 v-if="error.message" >{{ error.message }}</h2>
    </div>
    <div>
      <button type="submit" v-on:click="login()">LOGIN</button>
    </div>
    <br>
    <a href="">Forgot password?</a>
  </div>
</template>

<script>

export default {
  name: 'Login',
  user: {
    loggedIn: false,
    username: null,
    accessToken: null,
    refreshToken: null,
  },
  data: function () {
    return {
      api: {
        body: {
          username: "",
          password: "",
        },
        host: 'https://stage.apis.chatbot.gavagai.io',
        basePath: '/api/v1',
      },
      loading: false,
      error: {
        message: '',
      }
    }
  },
  methods: {
    login() {
      this.loading = true;
      const { host, basePath, body } = this.api;
      const apiPath = host + basePath + '/login';
      const optionsobj = {
        method: "POST",
        headers: {
          "Content-Type" : "application/json",
        },
        body: JSON.stringify(body),
      };
      fetch(apiPath, optionsobj)
        .then(response => response.json())
        .then(data => {
          const { access_token, refresh_token, Message } = data;
          this.error.message = Message;
          if (access_token && refresh_token) {
            localStorage.setItem('access_token', access_token);
            localStorage.setItem('refresh_token', refresh_token);
          }
          this.loading = false;
      });
    }
  },
}
</script>

<style>
h1 {
  font-weight: 100;
  font-style: italic;
  margin-top: 0px;
  margin-bottom: 45px;
}
h2 {
  font-weight: 100;
  font-style: italic;
  margin-top: 0px;
}
input {
  width: 60%;
  padding: 12px 3px;
  margin: 0px 0;
  box-sizing: border-box;
  outline: 0;
  border-width: 0 0 2px;
  border-color: black;
}
.title {
  text-align: left;
  margin-left: 120px;
  margin-top: 10px;
  opacity: 0.5;
}
.fas {
  margin-right: 10px;
}
#logincomponent {
  height: 520px;
  width: 500px;
  background-color: white;
}
.logo {
  height: 100px;
}
.loader_error {
  margin-bottom: 5px;
  margin-top:10px;
  height: 60px;
}
button {
  background-color: black;
  color: white;
  height: 50px;
  width: 160px;
  margin-top: 0px;
  font-size: 20px;
  font-weight: 100;
}
.lds-ring {
  display: inline-block;
  position: relative;
  width: 64px;
  height: 64px;
}
.lds-ring div {
  box-sizing: border-box;
  display: block;
  position: absolute;
  width: 51px;
  height: 51px;
  margin: 6px;
  border: 6px solid #fff;
  border-radius: 50%;
  animation: lds-ring 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  border-color: #f4f4f4 transparent transparent transparent;
}
.lds-ring div:nth-child(1) {
  animation-delay: -0.45s;
}
.lds-ring div:nth-child(2) {
  animation-delay: -0.3s;
}
.lds-ring div:nth-child(3) {
  animation-delay: -0.15s;
}
@keyframes lds-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
