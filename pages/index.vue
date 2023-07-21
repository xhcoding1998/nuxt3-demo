<script setup lang="ts">
  useHead({
    meta: {
      title: '首页'
    }
  })

  import { useRouter } from 'vue-router'
  import { useDiscuss, type IDiscuss, type IDiscussItem } from '@/hooks/index'

  const router = useRouter()
  const discuss = useDiscuss() as IDiscuss

  const handleToDetail = (item: IDiscussItem) => {
    router.push({
      path: 'detail',
      query: {
        id: item.id
      }
    })
  }
</script>

<template>
  <div class="discuss-card">
    <h1 v-html="discuss.title"></h1>
    <div class="discuss-list">
      <div
        v-for="(item, idx) in discuss.list"
        :key="idx"
        class="discuss-item">
        <a @click="handleToDetail(item)">查看完整歌词</a>
        <img :src="item.img">
        <span class="user-name">{{ item.name }}</span>
        <p class="user-des">{{ item.des }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
  h1 {
    text-align: center;
    margin-bottom: 50px;
    color: burlywood;
  }
  a {
    cursor: pointer;
    position: absolute;
    top: 20px;
    right: 20px;
    text-decoration: underline;
    color: cornflowerblue;
  }
  .discuss-card {
    width: 700px;
    margin: 100px auto;
  }
  .discuss-list {
    display: grid;
    grid-template-columns: repeat(1, 1fr);
    gap: 20px;
  }
  .discuss-item {
    padding: 20px;
    box-shadow: 0 0 5px #ccc;
    border-radius: 20px;
    transition: all 200ms;
    position: relative;
  }
  .discuss-item:hover {
    box-shadow: 5px 5px 20px #ccc;
  }
  .discuss-item img {
    width: 60px;
    height: 60px;
  }
  .discuss-item .user-name {
    margin-left: 20px;
    font-weight: bold;
    font-size: 24px;
  }
  .discuss-item .user-des {
    margin-top: 30px;
  }
</style>