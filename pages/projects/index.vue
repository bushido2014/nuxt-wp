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
  async asyncData({ $axios }) {
    let projects = await $axios.$get('/wp-json/wp/v2/project');
    projects = projects.map(
      ({ id, slug, title, excerpt, featured_media_src_url }) => ({
        id,
        slug,
        title,
        excerpt,
        projectImg: featured_media_src_url,
      })
    );
    return { projects };
  },
  head() {
    return {
      title: 'All projects - Nuxt WP',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Website  Development, Vue, Nuxt.js and WordPress ',
        },
      ],
    };
  },
};
</script>
