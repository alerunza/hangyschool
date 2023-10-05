<script setup>
import { RouterLink, RouterView } from "vue-router";
import { getAuth } from "firebase/auth";
import { auth } from '@/firebase.js';
import { onMounted, ref } from "vue";
const emit = defineEmits(['toggleTheme'])

const isLoggedIn = ref(false);
const isEmailVerified = ref(false);

function checkEmailVerification() {
  const user = getAuth().currentUser;
  isLoggedIn.value = user !== null;

  if (user) {
    isEmailVerified.value = user.emailVerified;
  } else {
    isEmailVerified.value = false;
  }

  console.log(
    `L'utente è ${isLoggedIn.value ? "loggato" : "non loggato"} e ${isEmailVerified.value ? "ha" : "non ha"
    } verificato l'email.`
  );

  return isLoggedIn.value && !isEmailVerified.value;
}

const unsubscribe = auth.onAuthStateChanged(() => {
  checkEmailVerification();
});

onMounted(() => {
  unsubscribe();
})
</script>

<script>
export default {
  data() {
    return {
    };
  },
  methods: {
    changeLocale(locale) {
      this.$i18n.locale = locale;
      this.$emit("locale-changed", locale);
    },
  }
}
</script>

<template>
  <div class="d-flex justify-content-center">
    <div class="dropdown fs-2 mt-1">
      <button class="btn dropdown-toggle" type="button" id="dropdownMenuButton2" data-bs-toggle="dropdown"
        aria-expanded="false">
        <i class="bi bi-translate text-info"></i> {{ $i18n.locale }}
      </button>
      <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton2">
        <li v-for="locale in $i18n.availableLocales" :key="locale">
          <a :class="locale === $i18n.locale ? 'dropdown-item active' : 'dropdown-item'" class="dropdown-item" href="#"
            @click="changeLocale(locale)">
            {{ locale }}
          </a>
        </li>
      </ul>
    </div>
    <RouterLink v-if="$route.path !== '/profile'" to="/profile"
      class="btn-link fs-2 text-decoration-none position-relative py-1 px-2"><i class="bi bi-person-circle"></i>
    </RouterLink>
    <RouterLink v-if="$route.path !== '/'" to="/" class="btn-link fs-2 text-decoration-none position-relative py-1 px-2">
      <i class="bi bi-house-fill"></i>
    </RouterLink>
  </div>
</template>

<style>
[theme="custom-dark"] {
  background: #16171d !important;
  color: #fff;
}

[theme="custom-dark"] nav {
  background: #16171d !important;
  color: #fff;
  border-bottom: 0.5px solid white !important;
}

[theme="custom-dark"] #dropdownMenuButton2 {
  color: #fff !important;
}

[theme="custom-dark"] .dropdown-menu {
  background-color: #16171d !important;
  border: #fff 1px solid !important;
}

[theme="custom-dark"] .dropdown-toggle-split {
  color: #ffffff !important;
}

[theme="custom-dark"] a.router-link-active {
  color: #ef5454 !important;
}

[theme="custom-dark"] .dropdown-item {
  color: #fff !important;
}

[theme="custom-dark"] #home {
  background: #16171d !important;
  color: #ffffff;
}

[theme="custom-dark"] .card {
  background: #43454e !important;
  color: #ffffff;
}

[theme="custom-dark"] .card:hover {
  box-shadow: 0 8px 50px #ef3c3c33 !important;
}

[theme="custom-dark"] .card .card-title {
  color: #ffffff;
}

[theme="custom-dark"] .t-lead {
  color: #ffffff;
}

[theme="custom-dark"] #keyboard {
  background-color: #43454e !important;
  color: #16171d;
}

[theme="custom-dark"] .toast-body {
  background-color: #43454e !important;
  border-radius: 5px;
}
</style>

<style scoped>
.dropdown-menu {
  min-width: 7.2rem;
}

.dropdown-item.active {
  background-color: #e64343;
}

.selectpicker {
  border: none;
}

/* .btn {
  border: none;
}
 */
.btn:hover {
  color: #b33636;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
}

a.dropdown-item:active {
  background-color: #ec9c9c;
}

a.nav-link:hover {
  color: #b33636;
}

.nav-item a {
  color: #ff4d4d;
}

.deactivated {
  color: #ff4d4d;
}

.nav-item.active a {
  font-weight: bold;
}

a.router-link-active {
  font-weight: bold;
  color: #b33636;
}

.btn-link {
  color: #ff4d4d;
}

.btn-link:hover {
  color: #b33636;
}

nav {
  border-bottom: 0.5px solid black;
  backdrop-filter: blur(10px);
}

.small-badge {
  font-size: 0.7rem;
}
</style>
