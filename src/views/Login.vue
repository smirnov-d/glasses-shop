<script setup lang="ts">
import { onMounted, ref } from 'vue';
import axios from 'axios';
import router from '@/router';

// defineProps<{
//   msg: string;
// }>();

const email = ref("dim-on-94@mail.ru");
const password = ref("qweasd");
const error = ref(null);

const loading = ref(false);

async function login(e): Promise<boolean> {
  try {
    loading.value = true
    const { data } = await axios.post('http://localhost:8080/auth/login', {
      email: email.value,
      password: password.value,
    });

    const token = data.access_token;

    localStorage.setItem('token', token);

    console.log(token);

    await router.replace('/');
  } catch (e) {
    // todo: ??
    error.value = e;
  } finally {
    loading.value = false;
  }




  // localStorage.setItem('token', token);

  // console.log('res', res);
  // console.log(email.value, pass.value);
  return true;
}

// function fetchData() {
//   loading.value = true;
//   // I prefer to use fetch
//   // you can use use axios as an alternative
//   return fetch('http://jsonplaceholder.typicode.com/posts', {
//     method: 'get',
//     headers: {
//       'content-type': 'application/json'
//     }
//   })
//       .then(res => {
//         // a non-200 response code
//         if (!res.ok) {
//           // create error instance with HTTP status text
//           const error = new Error(res.statusText);
//           error.json = res.json();
//           throw error;
//         }
//
//         return res.json();
//       })
//       .then(json => {
//         // set the response data
//         data.value = json.data;
//       })
//       .catch(err => {
//         error.value = err;
//         // In case a custom JSON error response was provided
//         if (err.json) {
//           return err.json.then(json => {
//             // set the JSON response message
//             error.value.message = json.message;
//           });
//         }
//       })
//       .then(() => {
//         loading.value = false;
//       });
// }

// onMounted(() => {
//   fetchData();
// });

</script>

<template>
  <main>
    {{ email }} - {{ password }}
    <div v-if="loading">Loading</div>
    <form v-else @submit.prevent="login">
      <div>
        <input type="email" v-model="email" />
      </div>
      <div>
        <input type="password" v-model="password" />
      </div>
      <button>Login</button>
    </form>
    <div v-if="error">{{ error }}</div>
  </main>
</template>
