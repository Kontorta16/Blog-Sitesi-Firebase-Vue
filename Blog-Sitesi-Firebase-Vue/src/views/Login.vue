<template>
  <div class="form-wrap">
    <form class="login">
      <h2>FireBlog Giriş</h2>
      <p class="login-register">Don't have an account?
        <router-link class="router-link" :to="{name: 'Register'}">Kayıt Ol</router-link>
      </p>
      <div class="inputs">
        <div class="input">
          <input type="text" placeholder="Email" v-model="email"/>
          <Email class="icon"/>
        </div>
        <div class="input">
          <input type="password" placeholder="Şifre" v-model="password"/>
          <Password class="icon"/>
        </div>
        <div class="error" v-show="error">{{ this.errorMsg }}</div>
      </div>
      <router-link class="forgot-password" :to="{name: 'ForgotPassword'}">Şifremi Unuttum</router-link>
      <button @click.prevent="login">Giriş Yap</button>
      <div class="angle"></div>
    </form>
    <div class="background"></div>
  </div>
</template>

<script>
import Email from "../assets/Icons/envelope-regular.svg";
import Password from "../assets/Icons/lock-alt-solid.svg";
import "firebase/auth";
import firebase from "firebase";

export default {
  name: "Login",
  components: {Email, Password},
  data() {
    return {
      email: null,
      password: null,
      error: null,
      errorMsg: "",
    }
  },
  methods: {
    login() {
      if (this.email !== "" || this.password !== "") {
        firebase.auth().signInWithEmailAndPassword(this.email, this.password)
            .then(() => {
              this.$router.push({name: "Home"})
              this.error = false;
              this.errorMsg = "";
            })
            .catch(error => {
              this.error = true;
              this.errorMsg = error.message
            })
        return;
      }
      this.error = true;
      this.errorMsg = "Please Fill out all the fields!";
    }
  }
}
</script>

<style>
.form-wrap {
  overflow: hidden;
  display: flex;
  height: 100vh;
  justify-content: center;
  align-self: center;
  margin: 0 auto;
  width: 90%;
}

.form-wrap .login-register {
  margin-bottom: 32px;
}

.form-wrap .login-register .router-link {
  color: #000;
}

.form-wrap form {
  padding: 0 10px;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  flex: 1;
}

.form-wrap form h2 {
  text-align: center;
  font-size: 32px;
  color: #303030;
  margin-bottom: 40px;
}

.form-wrap form .inputs {
  width: 100%;
  max-width: 350px;
}

.form-wrap form .inputs .input {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 8px;
}

.form-wrap form .inputs .input input {
  width: 100%;
  border: none;
  background-color: #f2f7f6;
  padding: 4px 4px 4px 30px;
  height: 50px;
}

.form-wrap form .inputs .input input:focus {
  outline: none;
}

.form-wrap form .inputs .input .icon {
  width: 12px;
  position: absolute;
  left: 6px;
}

.form-wrap form .forgot-password {
  text-decoration: none;
  color: #000;
  cursor: pointer;
  font-size: 14px;
  margin: 16px 0 32px;
  border-bottom: 1px solid transparent;
  transition: .5s ease all;
}

.form-wrap form .forgot-password:hover {
  border-color: #303030;
}

.form-wrap form .angle {
  display: none;
  position: absolute;
  background-color: #ffffff;
  transform: rotateZ(3deg);
  width: 60px;
  right: -30px;
  height: 101%;
}

.form-wrap .background {
  display: none;
  flex: 2;
  background-size: cover;
  background-image: url("../assets/background.png");
  width: 100%;
  height: 100%;
}

@media (min-width: 900px) {
  .form-wrap {
    width: 100%;
  }

  .form-wrap form {
    padding: 0 50px;
  }

  .form-wrap form h2 {
    font-size: 40px;
  }

  .form-wrap form .angle {
    display: initial;
  }

  .form-wrap .background {
    display: initial;
  }
}
</style>













