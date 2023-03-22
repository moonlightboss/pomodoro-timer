<template>
  <v-app>
    <v-container>
      <v-row>
        <v-col sm="6" offset-sm="3">
          <PomodoroClock/>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
import PomodoroClock from './components/PomodoroClock.vue';

export default {
  name: 'App',

  components: {
    PomodoroClock,
  },

  data: () => ({
    //
  }),
}
</script>
