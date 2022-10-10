<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  >
  </main-screen>

  <InteractScreen v-if="statusMatch === 'match'" :cardsContext="settings.cardsContext"> </InteractScreen>
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import  {shuffled} from "./utils/array.js"
export default {
  name: "App",
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        startedAt: null,
        cardsContext: [],
      },
      statusMatch: "default",
    };
  },
  components: {
    MainScreen,
    InteractScreen,
  },
  methods: {
    onHandleBeforeStart(config) {
      this.settings.totalOfBlocks = config.totalOfBlocks;
      const fistCards = Array.from(
        {
          length: this.settings.totalOfBlocks / 2,
        },
        (_, i) => i + 1
      );
      const secondCards = fistCards;
      const cards = [...fistCards, ...secondCards];

      this.settings.cardsContext = shuffled(shuffled(shuffled(shuffled(cards))));
      this.settings.startedAt = new Date().getTime();
      this.statusMatch = "match";
    },
  },
};
</script>
