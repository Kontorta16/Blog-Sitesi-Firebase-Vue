<template>
  <div class="profile">
    <Modal v-if="modalActive" :modalMessage="modalMessage" v-on:close-modal="closeModal"/>
    <div class="container">
      <h2>Hesap Ayarları</h2>
      <div class="profile-info">
        <div class="initials">{{ $store.state.profileInitials }}</div>
        <div class="admin-badge">
          <adminIcon class="icon"/>
          <span>Admin</span>
        </div>
        <div class="input">
          <label for="firstName">Adınız: </label>
          <input type="text" id="firstName" v-model="firstName"/>
        </div>
        <div class="input">
          <label for="lastName">Soyadınız: </label>
          <input type="text" id="lastName" v-model="lastName"/>
        </div>
        <div class="input">
          <label for="userName">Kullanıcı Adınız: </label>
          <input type="text" id="userName" v-model="userName"/>
        </div>
        <div class="input">
          <label for="email">Email: </label>
          <input disabled type="text" id="email" v-model="email"/>
        </div>
        <button @click="updateProfile">Değişiklikleri Kaydet</button>
      </div>
    </div>
  </div>
</template>

<script>
import Modal from "@/components/Modal";
import adminIcon from "../assets/Icons/user-crown-light.svg";

export default {
  name: "Profile",
  components: {Modal, adminIcon},
  data() {
    return {
      modalActive: null,
      modalMessage: "Changes were Saved!",
    }
  },
  methods: {
    closeModal() {
      this.modalActive = false;
    },
    updateProfile() {
      this.$store.dispatch("updateUserSettings");
      this.modalActive = !this.modalActive;
    },
  },
  computed: {
    firstName: {
      get() {
        return this.$store.state.profileFirstName;
      },
      set(payload) {
        this.$store.commit("changeFirstName", payload);
      }
    },
    lastName: {
      get() {
        return this.$store.state.profileLastName;
      },
      set(payload) {
        this.$store.commit("changeLastName", payload);
      }
    },
    email: {
      get() {
        return this.$store.state.profileEmail;
      },
      set(payload) {
        this.$store.commit("changeEmail", payload);
      }
    },
    userName: {
      get() {
        return this.$store.state.profileUserName;
      },
      set(payload) {
        this.$store.commit("changeUserName", payload);
      }
    },
  }
}
</script>

<style scoped>
.profile .container {
  max-width: 1000px;
  padding: 60px 25px;
}

.profile .container h2 {
  text-align: center;
  margin-bottom: 16px;
  font-weight: 300;
  font-size: 32px;
}

.profile .container .profile-info {
  border-radius: 8px;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  padding: 32px;
  background-color: #f1f1f1;
  display: flex;
  flex-direction: column;
  max-width: 600px;
  margin: 32px auto;
}

.profile .container .profile-info .initials {
  position: initial;
  width: 80px;
  height: 80px;
  font-size: 32px;
  background-color: #303030;
  color: #fff;
  display: flex;
  align-self: center;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
}

.profile .container .profile-info .admin-badge {
  display: flex;
  align-self: center;
  color: #fff;
  font-size: 14px;
  padding: 8px 24px;
  border-radius: 8px;
  background-color: #303030;
  margin: 16px 0;
  text-align: center;
  text-transform: capitalize;
}

.profile .container .profile-info .admin-badge .icon {
  width: 14px;
  height: auto;
  margin-right: 8px;
}

.profile .container .profile-info .input {
  margin: 16px 0;
}

.profile .container .profile-info .input label {
  font-size: 14px;
  display: block;
  padding-bottom: 6px;
}

.profile .container .profile-info .input input {
  width: 100%;
  border: none;
  background-color: #f2f7f6;
  padding: 8px;
  height: 50px;
}

.profile .container .profile-info .input input:focus {
  outline: none;
}

.profile .container .profile-info button {
  align-self: center;
}

@media (min-width: 900px) {
  .profile .container .profile-info .input input {

  }
}


</style>
