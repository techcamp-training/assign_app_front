<script setup>
import { auth, createUserWithEmailAndPassword,updateProfile } from '../firebase';
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const email = ref('');
const password = ref('');
const currentUser = ref(null);
const router = useRouter();

const handleSignUp = async() => {
  try {
    // 入力された情報を元に、ユーザー登録する
    const credentialUser = await createUserWithEmailAndPassword(auth, email.value, password.value)

    router.push("/top");
  }catch(error) {
    console.log('ユーザー登録できませんでした', error)
  }
}
</script>

<template>
  <h1>新規登録</h1>
  <form>
    <input type="text" id="email" placeholder="email" v-model="email">
    <input type="password" id="password" placeholder="password" v-model="password">
    <button @click.prevent="handleSignUp">新規登録</button>
  </form>
  <p>既にアカウントをお持ちの方は<router-link to="/">こちら</router-link>へ</p>
</template>