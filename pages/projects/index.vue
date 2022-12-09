<template>
  <section class="all-projects">
    <div class="container">
      <div v-if="projects" class="project-wrapper grid">
        <ProjectCard
          v-for="(project, i) in projects"
          :key="i"
          :project="project"
        />
      </div>
    </div>
  </section>
</template>

<script>
import ProjectCard from '~/components/ProjectCard';
export default {
  components: { ProjectCard },
  async getAllProjects({ $axios }) {
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
      link: [
        {
          rel: 'canonical',
          href: 'https://dev-websoltan.com' + this.$route.path,
        },
      ],
    };
  },
};
</script>
