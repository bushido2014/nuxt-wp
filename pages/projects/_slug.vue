<template>
  <div class="container">
    <article
      v-for="project in projects"
      :key="project.id"
      class="single-project"
    >
      <div class="single-project-title">
        <h1>
          {{ project.title.rendered }}
        </h1>
      </div>
      <div class="single-project-content">
        <div
          v-if="project.content"
          class="mt-5 content"
          v-html="project.content.rendered"
        ></div>
      </div>
    </article>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, params, error }) {
    const project = await $axios.$get(
      '/wp-json/wp/v2/project/?slug=' + params.slug + '&_embed=1'
    );
    if (project.length <= 0) {
      return error({ statusCode: 404, message: 'Page not found' });
    }
    console.log(project[0]);
    return { project: project[0] };
  },

  head() {
    return {
      title: this.project[0].title.rendered,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.project[0].excerpt.rendered,
        },
        {
          hid: 'og:title',
          property: 'og:title',
          content: this.project[0].title.rendered,
        },
        {
          hid: 'og:description',
          property: 'og:description',
          content: this.project[0].excerpt.rendered,
        },
        {
          hid: 'og:type',
          property: 'og:type',
          content: 'project',
        },
      ],
    };
  },
};
</script>
