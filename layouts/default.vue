<template>
  <div>
    <Header />
    <transition name="fade" mode="out-in">
      <Nuxt />
    </transition>
    <Footer />

    <div class="back"></div>
  </div>
</template>
<script>
import Header from '~/components/Header';
import Footer from '~/components/Footer';

export default {
  components: {
    Header,
    Footer,
  },
};
</script>
