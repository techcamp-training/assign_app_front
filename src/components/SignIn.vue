<script setup>
import { auth, signInWithEmailAndPassword } from '../firebase';
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const email = ref('');
const password = ref('');
const currentUser = ref(null);
const router = useRouter();

const handleSignIn = async() => {
  try {
    const credentialUser = await signInWithEmailAndPassword(auth, email.value, password.value)
    currentUser.value = credentialUser.user;

    router.push("/top");
  }catch(error) {
    console.log('ログインできませんでした',error)
  }
}

</script>

<template>
  <h1>ログイン</h1>
  <form>
    <input type="text" id="email" placeholder="email" v-model="email">
    <input type="password" id="password" placeholder="password" v-model="password">
    <button @click.prevent="handleSignIn">ログイン</button>
  </form>
  <p>アカウント作成がお済みでない場合は、<router-link to="/signup">こちら</router-link>へ</p>
</template>