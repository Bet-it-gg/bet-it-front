<template>
  <v-container>
    <!--    <div v-if="getuser.id != null">-->
    <v-row class="d-flex justify-end">
<!--      <div-->
<!--          class="d-flex justify-end align-center"-->
<!--          v-if="getuser.betties >= 1 && getuser.betties < 30"-->
<!--      >-->
<!--        <span class="amount text-h3 mr-5">{{ getuser.betties }}</span>-->
<!--        <img style="width: 100px" src="../assets/monney/tas.svg" alt="monnaie" />-->
<!--      </div>-->
<!--      <div-->
<!--          class="d-flex justify-end align-center"-->
<!--          v-else-if="getuser.betties >= 30 && getuser.betties < 60"-->
<!--      >-->
<!--        <span class="amount text-h3 mr-5">{{ getuser.betties }}</span>-->
<!--        <img style="width: 100px" src="../assets/monney/tasUp.svg" alt="monnaie" />-->
<!--      </div>-->
<!--      <div-->
<!--          class="d-flex justify-end align-center"-->
<!--          v-else-if="getuser.betties >= 60 && getuser.betties < 150"-->
<!--      >-->
<!--        <span class="amount text-h3 mr-5">{{ getuser.betties }}</span>-->
<!--        <img style="width: 100px" src="../assets/monney/bourse.svg" alt="monnaie" />-->
<!--      </div>-->
<!--      <div-->
<!--          class="d-flex justify-end align-center"-->
<!--          v-else-if="getuser.betties >= 150"-->
<!--      >-->
<!--        <span class="amount text-h3 mr-5">{{ getuser.betties }}</span>-->
<!--        <img style="width: 100px" src="../assets/monney/coffre.svg" alt="monnaie" />-->
      <BettiesSold />
    </v-row>

      <v-row class="mt-12 justify-center">
        <v-col cols="12" md="6" class="d-flex flex-column align-center">
          <v-card
              color="white"
              class="game-card mt-10"
              width="200"
              height="200"
              outlined
          >
            <div
                class="d-flex align-center div-text w-100 justify-space-between"
            >
              <v-img class="mx-2" :src="event.team1.logo" width="80"></v-img>
              <div class="line"></div>
              <v-img class="mx-2" :src="event.team2.logo" width="80"></v-img>
            </div>
          </v-card>
          <v-card
              color="white"
              class="games-history d-flex flex-column align-center mt-12"
          >
            <div class="text-h3 text-center my-3">Derniers matchs</div>
            <div class="d-flex justify-center flex-wrap">
              <GameHistory :event="event" />
            </div>
          </v-card>
        </v-col>

        <v-col cols="12" md="6">
          <v-card class="bet-types" color="white">
            <v-card-title class="card-title text-h4"
            >Paris à venir</v-card-title
            >
            <div class="pa-2 bet-types-list overflow-y-auto">
              <BetType v-for="(bet, idx) in bets" :key="idx" :bet="bet" />
            </div>
          </v-card>
        </v-col>
      </v-row>
<!--    </div>-->
    <!--    <div v-else>-->
    <!--      <NotConnected></NotConnected>-->
    <!--    </div>-->
  </v-container>
</template>

<script>
import BetType from "@/components/Bet/BetType";
import GameHistory from "@/components/Bet/GameHistory";
import store from "@/store/index.js";
import BettiesSold from '@/components/BettiesSold';
//import NotConnected from "@/components/NotConnected.vue";

export default {
  store: store,

  components: {
    BetType,
    GameHistory,
    BettiesSold
    //NotConnected,
  },
  data: () => ({
    bets: [],
  }),
  computed: {
    // betties() {
    //   return this.$store.state.betties;
    // },

    event() {
      return this.$store.state.event;
    },
    getuser() {
      return this.$store.state.user;
    },
  },

  mounted: async function () {
    store.dispatch("getEventId", this.$route.params.id);

    this.bets = [
      {
        id: "0-" + this.event.team1.name + "'-W",
        type: "Winner",
        team: this.event.team1,
        odd: 1.1,
        game: {
          id: this.event.id,
          team1: this.event.team1,
          team2: this.event.team2,
          gameNumber: 1,
          league: "LEC",
        },
      },
      {
        id: "0-" + this.event.team2.name + "-W",
        type: "Winner",
        team: this.event.team2,
        odd: 2,
        game: {
          id: this.event.id,
          team1: this.event.team1,
          team2: this.event.team2,
          gameNumber: 1,
          league: "LEC",
        },
      },
      {
        id: "0-" + this.event.team1.name + "-FB",
        type: "First Blood",
        team: this.event.team1,
        odd: 1.1,
        game: {
          id: this.event.id,
          team1: this.event.team1,
          team2: this.event.team2,
          gameNumber: 1,
          league: "LEC",
        },
      },
      {
        id: "0-" + this.event.team2.name + "-FB",
        type: "First Blood",
        team: this.event.team2,
        odd: 2,
        game: {
          id: this.event.id,
          team1: this.event.team1,
          team2: this.event.team2,
          gameNumber: 1,
          league: "LEC",
        },
      },
      {
        id: "0-" + this.event.team1.name + "-FT",
        type: "First Turret",
        team: this.event.team1,
        odd: 1.1,
        game: {
          id: this.event.id,
          team1: this.event.team1,
          team2: this.event.team2,
          gameNumber: 1,
          league: "LEC",
        },
      },
      {
        id: "0-" + this.event.team2.name + "-FT",
        type: "First Turret",
        team: this.event.team2,
        odd: 2,
        game: {
          id: this.event.id,
          team1: this.event.team1,
          team2: this.event.team2,
          gameNumber: 1,
          league: "LEC",
        },
      },
    ];
  },
};
</script>

<style lang="scss" scoped>
.bet-types,
.games-history {
  background: #303030 !important;
}

.bet-types-list {
  height: 560px;
}

.games-history {
  width: 1000px;
  min-height: 250px;
}

.card-title,
.bet-btn {
  background: linear-gradient(
          0.25turn,
          var(--v-darkPurple-base),
          var(--v-info-base),
          var(--v-secondary-base)
  );
  text-transform: none;
}

.line {
  height: 13rem;
  border: 1px solid;
}

.div-text {
  transform: rotate(-45deg);
  transform-origin: center;
}

.game-card {
  transform: rotate(45deg);
  transform-origin: center;
  transition: 0.4s ease-in-out;
  color: grey;
}
</style>
