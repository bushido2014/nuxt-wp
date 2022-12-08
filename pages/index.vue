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
  </div>
</template>

<script>
import Hero from '~/components/Hero';
import Skills from '~/components/Skills';
export default {
  components: { Hero, Skills },
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
