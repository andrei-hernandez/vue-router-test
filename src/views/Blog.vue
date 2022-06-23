<template>
  <div>
    <Title title="Titulo de mi blog"/>
    <button @click="getPosts">Consume API</button>
    <div v-for="post in blogPosts" :key="post.id">
      <router-link :to="`/blog/${post.id}`">
        {{ post.title }}
      </router-link>
    </div>
  </div>
</template>

<script lang="ts">
import Title from '@/components/Title.vue';
import { defineComponent } from 'vue';
import { Post } from '@/models';

export default defineComponent({
  name: 'blog-view',
  components: {
    Title,
  },
  data() {
    return {
      blogPosts: [] as Post[],
    };
  },
  methods: {
    async getPosts(): Promise<void> {
      try {
        const data = await fetch('https://jsonplaceholder.typicode.com/posts');
        const posts: Array<Post> = await data.json();
        this.blogPosts = posts;
      } catch (error) {
        // eslint-disable-next-line no-console
        console.log(error);
      }
    },
  },
  created() {
    this.getPosts();
  },
});
</script>

<style>

</style>
