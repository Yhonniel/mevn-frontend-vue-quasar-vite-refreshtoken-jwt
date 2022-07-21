<template>
  <q-page padding>
    <q-btn @click="userStore.access">INGRESAR</q-btn>
    <q-btn @click="createLink">Crear Link</q-btn>
    <q-btn @click="userStore.logout">Cerrar Sesión</q-btn>
    {{ userStore.token }} - {{ userStore.expireIn }}
  </q-page>
</template>

<script setup>
//import axios from "axios";
import { api } from "src/boot/axios";

import { useUserStore } from "../stores/user-store";

const userStore = useUserStore();

//userStore.refreshToken();

// const access = () => {
//   console.log("access");
//   axios
//     .post("http://localhost:3001/api/v1/auth/login", {
//       email: "rigo@test.com",
//       password: "123123",
//     })
//     .then((res) => {
//       console.log(res.data);
//     })
//     .catch((e) => console.log(e));
// };

const createLink = async () => {
  try {
    const res = await api({
      method: "POST",
      url: "/links",
      headers: {
        Authorization: "Bearer " + token.value,
      },
      data: {
        longLink: "https://www.google.com",
      },
    });
    console.log(res.data);
  } catch (error) {
    console.log(error);
  }
};
</script>
