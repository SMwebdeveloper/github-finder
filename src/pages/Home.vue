<template lang="">
  <div class="wrapper-content wrapper-content--fixed home">
    <section>
      <div class="container">
        <search
          :value="search"
          placeholder="Type username..."
          @search="search = $event"
        />

        <!-- buttons -->
        <button v-if="!repos" class="btn-primary" @click="getRepos">Search!</button>
        <button v-else class="btn-primary" @click="getRepos">Search Again!</button>

        <div class="error" v-if="error">
          <p>{{ error }}</p>
        </div>

        <!-- repos wrapper -->
        <div class="repos__wrapper" v-if="repos">
          <!-- item -->
          <div class="repos__item" v-for="repo in repos" :key="repo.id">
            <div class="repo-info">
              <a class="link" :href="repo.html_url" target="_blank">{{
                repo.name
              }}</a>
              <span>{{ repo.stargazers_count }} ⭐</span>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
<script>
import search from "@/components/Search.vue";
import axios from "axios";
export default {
  components: {
    search,
  },
  data() {
    return {
      search: "",
      error: null,
      repos: null,
    };
  },
  methods: {
    getRepos() {
      axios
        .get(`https://api.github.com/users/${this.search}/repos`)
        .then((res) => {
          console.log(res);
          this.repos = res.data;
          this.error = null
        })
        .catch((err) => {
          this.repos = null;
          this.error = `Can't find this user`
        });
    },
  },
};
</script>

<style lang="css" scoped>
.container {
  text-align: center;
}

.repos__wrapper {
  width: 500px;
  margin: 30px 0;
}

.repo-info {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 10px;
  padding: 10px 0;
  border-bottom: 1px solid #dbdbdb;
}
</style>
