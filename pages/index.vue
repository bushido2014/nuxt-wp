<template>
  <div>
    <Hero />
    <section class="skills" id="skills">
      <div class="section_title">
        <h1>SKILLS</h1>
      </div>
      <div class="container">
        <Skills />
      </div>
    </section>
    <section class="home-projects">
      <div class="section_title">
        <h1>Projects</h1>
      </div>
      <div class="container">
        <div class="project-list grid">
          <nuxt-link
            v-for="(project, i) in projects"
            :key="i"
            :to="`/project/${project.slug}/`"
            class="project-list__card"
          >
            <ProjectList :project="project" :no-text="true" />
          </nuxt-link>
        </div>
        <div class="project-list-link">
          <nuxt-link to="/project" class="button">View All Projects </nuxt-link>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import Hero from '~/components/Hero';
import Skills from '~/components/Skills';
import ProjectList from '~/components/ProjectList';
export default {
  components: { Hero, Skills, ProjectList },
  async getProjects({ $axios }) {
    const project = await $axios.$get('/wp-json/wp/v2/project?per_page=3');
    return { project };
  },
  head() {
    return {
      title: 'Viorel Soltan - Front End Developer',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Website with Nuxt.js and WordPress REST API',
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
