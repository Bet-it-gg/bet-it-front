<template>
  <v-container>
<!--    <div v-if="user.id != null">-->
    <div>
      <v-row justify="space-between">
        <v-col cols="12" md="6">
          <BetHistory />
        </v-col>
        <v-col cols="12" md="6">
          <BettiesAmount />
        </v-col>
      </v-row>
      <v-row class="my-5" no-gutters>
        <v-col>
          <AccountInfos />
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12" md="6">
          <AccountDeletion />
        </v-col>
      </v-row>
    </div>
<!--    <div v-else>-->
<!--      <NotConnected></NotConnected>-->
<!--    </div>-->
  </v-container>
</template>

<script>
import AccountInfos from "@/components/Profile/AccountInfos";
import AccountDeletion from "@/components/Profile/AccountDeletion";
import BetHistory from "@/components/Profile/BetHistory";
import BettiesAmount from "@/components/Profile/BettiesAmount";
import store from "@/store/index.js";
// import NotConnected from "@/components/NotConnected.vue";

export default {
  name: "Profile",
  store: store,

  components: {
    AccountInfos,
    AccountDeletion,
    BetHistory,
    BettiesAmount,
    // NotConnected,
  },
  computed: {
    user() {
      return store.state.user;
    },
  },
};
</script>

<style lang="scss">
.card-title,
.btn {
  background: linear-gradient(
    0.25turn,
    var(--v-darkPurple-base),
    var(--v-info-base),
    var(--v-secondary-base)
  );
  text-transform: none;
}

.icon {
  background-image: -webkit-linear-gradient(
    0.25turn,
    var(--v-darkPurple-base),
    var(--v-info-base),
    var(--v-secondary-base)
  );
  -webkit-text-fill-color: transparent;
}
</style>
