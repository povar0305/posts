<script lang="ts" setup>
const props = defineProps<{
  post: {
    title: string,
    author: {},
    body: string
  }
}>()
</script>

<template>
  <div class="post">
    <p class="title">{{ post.title }}</p>
    <p>{{ post.body }}</p>
    <p class="user">{{ post.author[0].name }}</p>
  </div>
</template>

<style lang="scss" scoped>

@import './assets/style/main.scss';

.post {
  display: flex;
  flex-direction: column;
  gap: 8px;
  border-radius: 8px;
  padding: 16px;
  background: $base-color;

  p {
    margin: 0;
  }


  .title {
    font-size: 1.2rem;
    color: $accent-color;
  }

  .user {
    font-size: 0.8rem;
    color: $gray-color;
  }
}
</style>