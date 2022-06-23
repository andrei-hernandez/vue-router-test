<template>
  <div>
    <Title title="Titulo de mi articulo"/>
    <h2>
      Param {{ $route.params.id }}
    </h2>
    <h3>
      {{ postData.title }}
    </h3>
    <p>
      {{ postData.body }}
    </p>
  </div>
</template>

<script lang="ts">
import Title from '@/components/Title.vue';
import { defineComponent } from 'vue';
import { Post } from '@/models';

export default defineComponent({
  name: 'blog-article',
  components: {
    Title,
  },
  data() {
    return {
      postData: {} as Post,
    };
  },
  methods: {
    async getPost(): Promise<void> {
      try {
        const data = await fetch(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`);
        const post: Post = await data.json();
        this.postData = post;
      } catch (error) {
        // eslint-disable-next-line no-console
        console.log(error);
      }
    },
  },
  created() {
    this.getPost();
  },
});
</script>

<style>

</style>
