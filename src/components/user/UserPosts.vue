<template>
  <div>
    <ul>
      <li v-for="post in posts" :key="post.id">{{post.title}}</li>
    </ul>
  </div>
</template>

<script>
import { API } from '../../utils/api';
export default {
  data() {
    return {
      posts: [],
    };
  },
  beforeRouteEnter(to, from, next) {
    console.log(to);
    API.get(`posts?userId=${to.params.userId}`)
      .then(response => next(vm => (vm.posts = response.data)))
      .catch(err => next(err));
  },
};
</script>