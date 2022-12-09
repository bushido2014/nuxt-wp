<template>
  <div>
    <div v-if="projects" class="container mx-auto my-20 px-6">
      <project-card
        v-for="(project, i) in projects"
        :key="i"
        :project="project"
      />
    </div>
  </div>
</template>
<script>
import ProjectCard from '~/components/ProjectCard';
export default {
  components: { ProjectCard },
  async asyncData({ $axios }) {
    const projects = await $axios.$get('/wp-json/wp/v2/project');
    return { projects };
  },
  head() {
    return {
      title: 'All Projects - Nuxt JS',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content:
            'Website  Development, Vue, Nuxt.js and WordPress Related Articles Related Articles, Tips , Web Hosting deals coupons and more.',
        },
      ],
    };
  },
};
</script>
