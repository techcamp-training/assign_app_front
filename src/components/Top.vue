<script setup>
import { auth, signOut } from '../firebase';
import { computed, onMounted, ref } from 'vue';
import { useRouter } from 'vue-router';
import  api from '../api/axios';
import TaskList from './TaskList.vue'

const router = useRouter();

const handleSignOut = async () => {
  await signOut(auth);
  router.push("/");
};

</script>

<template>
  <div class="header">
    <h1>タスク管理アプリ</h1>
    <button class="logout" @click="handleSignOut">ログアウト</button>
  </div>

  <form class="task-form">
    <div class="input-area">
      <label for="content">タスク内容</label>
      <textarea type="text" id="content" placeholder="content"></textarea>
    </div>

    <div class="input-area">
      <label for="assignee">対応者</label>
      <select>
        <option value="0">田中</option>
        <option value="1">山田</option>
        <option value="2">佐藤</option>
      </select>
    </div>

    <button class="submit-btn">保存</button>
  </form>
  <TaskList />
</template>

<style scoped>
.header {
  width: 500px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 24px;
}

.logout {
  width: 120px;
  height: 40px;
}

.task-form {
  display: flex;
  flex-direction: column;
  width: 500px;
  margin-top: 16px;
}

.input-area {
  display: flex;
  flex-direction: column;
  margin-bottom: 16px;
}

.submit-btn {
  width: 160px;
  margin: 0 auto;
}
</style>