<script setup>
import { ref } from 'vue';
import { RouterLink, RouterView } from 'vue-router'

const modalDialog = ref(null);

// タスクを追加する関数
const addTask = () => {
   if (newTask.value.name) {
      taskList.value.push({ ...newTask.value });
      newTask.value = {
         name: '',
         deadline: '',
         startTime: '',
         endTime: '',
         details: ''
      };
   }
   if (modalDialog.value) {
      modalDialog.value.classList.remove('open');
   }
};

// タスクを削除する関数
const removeTask = (index) => {
   taskList.value.splice(index, 1);
};

// モーダル開閉の関数
const openModal = () => {
   if (modalDialog.value) {
      modalDialog.value.classList.add('open');
   }
};

const closeModal = () => {
   if (modalDialog.value) {
      modalDialog.value.classList.remove('open');
   }
};
</script>

<template>
  <header>
    <nav>
      <h1><router-link to="/">TASK MANAGER</router-link></h1>
      <div class="bell alert">
        <img alt="通知" src="@/assets/bell.svg" width="25" height="25">
      </div>
    </nav>

    <div class="wrapper">
       <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>
  <main>
      <h2 class="date"><span>2023</span>09/09</h2>
      <ul>
         <li class="task-item">
            <span class="check checked"></span>
            <div>
               <p>ここにタスクが入ります。ここにタスクが入ります。ここにタスクが入ります。</p>
               <div class="bottom">
                  <span class="time">8:00 - 11:00</span>
                  <button class="edit">編集</button>
               </div>
            </div>
         </li>
         <li class="task-item">
            <span class="check"></span>
            <div>
               <p>ここにタスクが入ります。ここにタスクが入ります。ここにタスクが入ります。</p>
               <div class="bottom">
                  <span class="time">8:00 - 11:00</span>
                  <button class="edit">編集</button>
               </div>
            </div>
         </li>
         <li class="task-item">
            <span class="check"></span>
            <div class="inner">
               <p>ここにタスクが入ります。ここにタスクが入ります。ここにタスクが入ります。</p>
               <div class="bottom">
                  <span class="time">8:00 - 11:00</span>
                  <button class="edit">編集</button>
               </div>
            </div>
         </li>
      </ul>
      <h2 class="date"><span>2023</span>09/15</h2>
      <ul id="task">
         <li class="task-item" v-for="(task, index) in taskList" :key="index">
            <span class="check"></span>
            <div class="inner">
               <p>{{ task.name }}</p>
               <div class="bottom">
                  <div>{{ task.deadline }}</div>
                  <div class="time">{{ task.startTime }} - {{ task.endTime }}</div>
                  <!-- <button class="edit">編集</button> -->
                  <button @click="removeTask(index)" class="edit">削除</button>
               </div>
            </div>
         </li>
      </ul>
   </main>
   <button class="btn-plus" @click="openModal()"></button>

   <div class="modal" ref="modalDialog">
      <button class="btn-close" @click="closeModal()"></button>
      <label id="task">
         <input type="text" v-model="newTask.name" placeholder="タスクを追加してください" calus>
      </label>
      <label id="limit">
         <!-- <span class="icon"></span> -->
         <p>期限</p>
         <input type="date" v-model="newTask.deadline">
      </label>
      <label id="startTime">
         <!-- <span class="icon"></span> -->
         <p>開始時間</p>
         <input type="time" v-model="newTask.startTime">
      </label>
      <label id="endTime">
         <!-- <span class="icon"></span> -->
         <p>終了時間</p>
         <input type="time" v-model="newTask.endTime">
      </label>
      <label id="desc">
         <!-- <span class="icon"></span> -->
         <p>タスクの詳細</p>
         <textarea rows="7" placeholder="タスクの詳細を入力してください"></textarea>
      </label>
      <button class="btn-add" @click="addTask">タスクを追加</button>
   </div>
  <RouterView />
</template>


<style scoped>
header {
   padding: 1em;
   text-align: center;
   line-height: 1.5;
   max-height: 100vh;
   border-bottom: 1px solid #000;
}

nav {
   font-size: 14px;
   font-weight: 600;
   width: 100%;
   position: relative;
}

nav a.router-link-exact-active {
   color: var(--color-text);
}

nav a.router-link-exact-active:hover {
   background-color: transparent;
}

nav a {
   display: inline-block;
   padding: 0 1rem;
   border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
   border: 0;
}

main {
   padding: 50px 5%;
}

.bottom div {
   margin-top: 10px;
}



@media (min-width: 1024px) {
   .logo {
      margin: 0 2rem 0 0;
   }

   header .wrapper {
      display: flex;
      place-items: flex-start;
      flex-wrap: wrap;
   }

   nav {
      text-align: left;
      margin-left: -1rem;
      font-size: 1rem;

      padding: 1rem 0;
      margin-top: 1rem;
   }
}
</style>