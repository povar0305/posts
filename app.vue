<template>
  <div>
    <wrapper>
      <div class="search-row">
        <search-input v-model.trim="name"/>
      </div>
      <div class="wrapper">
        <div class="posts">
          <s-post v-for="post in filtredPosts" :post="post" :key="post.id"/>
          <p v-show="filtredPosts?.length==0" class="no-result">Увы, ничего не нашлось. Попробуйте изменить запрос.</p>
        </div>
      </div>

    </wrapper>
  </div>
</template>
<script lang="ts" setup>
import Wrapper from "~/components/wrapper.vue";
import axios from "axios";

const name = ref('')

const posts = ref(null)

function getAllPost() {

  axios.get('https://jsonplaceholder.typicode.com/posts')
      .then(response => {
        posts.value = response.data;
        for (let i in posts.value) {
              axios.get('https://jsonplaceholder.typicode.com/users?id='+posts.value[i].userId)
              .then(response => {
                posts.value[i].author= response.data[0].name
              })
        }
      })
}

getAllPost();


const filtredPosts = computed(() => {
  if (!name.value) {
    return posts.value
  } else {

    return posts.value.filter((post) => {
      return post.author.includes(name.value)
    })
  }
})
</script>

<style lang="scss">
@import './assets/style/main.scss';

body {
  margin: 0;
  padding: 0;
  background: $light-color;
}
</style>

<style lang="scss" scoped>
@import './assets/style/main.scss';

.search-row {
  display: flex;
  width: 100%;
  justify-content: center;
  position: sticky;
}

.wrapper {
  max-height: 92vh;
  overflow: scroll;
}

.posts {
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
  justify-content: space-around;

  .post {
    width: 100%;

    @media(min-width: 1024px) {
      max-width: 30%;
    }
    @media(min-width: 768px) {
      max-width: 40%;
    }

  }
}
</style>
