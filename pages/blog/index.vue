<template>
  <div class="container">
    <h2>All Posts</h2>
    <div v-if="posts" class="post-articles grid">
      <article-card v-for="(post, i) in posts" :key="i" class="" :post="post" />
    </div>
  </div>
</template>

<script>
import ArticleCard from '~/components/ArticleCard';

export default {
  components: { ArticleCard },
  async asyncData({ $axios }) {
    let posts = await $axios.$get(
      '/wp-json/wp/v2/posts?page=1&per_page=20&_embed=1'
    );
    posts = posts.map(({ id, slug, title, excerpt, _embedded }) => ({
      id,
      slug,
      title,
      excerpt,
      image: _embedded['wp:featuredmedia']['0'].source_url,
    }));
    return { posts };
  },
  head() {
    return {
      title: 'All Posts - Nuxt WP',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Home page description',
        },
      ],
    };
  },
};
</script>
