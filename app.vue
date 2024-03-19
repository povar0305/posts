<template>
  <div>
    <wrapper>
      <div class="search-row">
        <search-input v-model="name"/>
      </div>
      <div class="posts">
        <s-post v-for="post in filtredPosts" :post="post"/>
      </div>
    </wrapper>
  </div>
</template>
<script lang="ts" setup>
import Wrapper from "~/components/wrapper.vue";


const name = ref('')

const posts = ref(null)

function getAllPost() {
  fetch('https://jsonplaceholder.typicode.com/posts')
      .then(response => response.json())
      .then(json => posts.value = json)
}

getAllPost()


const users = ref(null)

function getAllUsers() {
  fetch('https://jsonplaceholder.typicode.com/users')
      .then(response => response.json())
      .then(json => users.value = json)
}

getAllUsers();

const filtredPosts = computed(() => {
  if (posts.value && users.value) {
    posts.value.map(function (post) {
      return post.author = users.value?.filter((user) => {

        if (post.userId == user.id)
          return user.name
      })
    })
  }


  if (!name.value) {
    return posts.value
  } else {

    return posts.value.filter((post) => {
      return post.author[0].name.includes(name.value)
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
.search-row {
  display: flex;
  width: 100%;
  justify-content: center;
}


.posts {
  display: flex;
  row-gap: 16px;
  flex-wrap: wrap;
  justify-content: space-around;

  .post {
    width: 30%;
  }
}
</style>
