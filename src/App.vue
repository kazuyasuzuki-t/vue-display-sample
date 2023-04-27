<template>
  <v-app>
    <v-main>
      <MainComponent />
    </v-main>
  </v-app>
</template>

<script>
import Main from './components/Main.vue';

export default {
  name: 'App',

  components: {
    MainComponent: Main,
  },

  data: () => ({
    //
  }),
};
</script>
