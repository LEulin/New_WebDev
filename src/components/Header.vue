<template>
  <div>
    <v-app-bar id="head" dark>
      <v-toolbar-title>
        <a @click="home()">
          <v-img :src="require('@/assets/logoSpotMe.png')"></v-img>
        </a>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-col cols="12" sm="3">
      <v-autocomplete
        v-show="$route.path === '/dashboard' || $route.path === '/bloggerdashboard'"
        v-model="select"
        :loading="loading"
        :items="items"
        :search-input.sync="search"
        cache-items
        class="mx-2"
        flat
        color="orange"
        prepend-inner-icon="mdi-magnify"
        hide-no-data
        hide-details
        label="e.g Hotel"
        solo-inverted
      ></v-autocomplete>
      </v-col>
      <v-btn
        text
        @click="signin()"
        v-show="$route.path === '/register' || $route.path === '/login'  || $route.path === '/'? true : false"
      >Sign up</v-btn>
      <v-btn
        text
        @click="login()"
        v-show="$route.path === '/register' || $route.path === '/login'  || $route.path === '/'? true : false"
      >Login</v-btn>
    </v-app-bar>
  </div>
</template>
<script>
export default {
  data() {
    return {
      loading: false,
      items: [],
      search: null,
      select: null,
      states: ["Hotel", "Mountain", "Beach Resort", "Historical"]
    };
  },
  watch: {
    search(val) {
      val && val !== this.select && this.querySelections(val);
    }
  },
  methods: {
    signin() {
      this.$router.push("/register");
    },
    login() {
      this.$router.push("/login");
    },
    home() {
      this.$router.push("/");
    },
    querySelections (v) {
        this.loading = true
        // Simulated ajax query
        setTimeout(() => {
          this.items = this.states.filter(e => {
            return (e || '').toLowerCase().indexOf((v || '').toLowerCase()) > -1
          })
          this.loading = false
        }, 500)
      },
  }
};
</script>

<style scoped>
#search {
  margin-top: 20px;
}
#head {
  padding-top: 2px;
  background-color: #cd853f;
}
</style>