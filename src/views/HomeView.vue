<template>
  <v-app class="home">
    <div  class="parent">
      <div class="link_commita" v-for="commit in commits" :key="commit.sha">
        <!-- <router-link :to="'/commit_details/' + commit.sha">{{ commit.sha }}</router-link> -->
        <router-link
          class="r_link"
          :to="{ name: 'commit_details', params: { sha: commit.sha } }"
          >{{ commit.sha }}</router-link
        >
      </div>
    </div>
  </v-app>
</template>

<script>
// @ is an alias to /src

export default {
  name: "HomeView",
  data() {
    return {
      commits: [],
    };
  },

  mounted: async function () {
    let get_request = await fetch(
      "https://api.github.com/repos/vuejs/vue/commits"
    );
    let response = await get_request.json(); //lokalna varijabla; vidljiva samo u mounted fun
    this.commits = response; //this se referencira na objekta kojeg sam eksportirao (export default ili data?)
  },
};
</script>

<style scoped>
.link_commita {
  background-color: rgb(57, 7, 67);
  margin: 10px; /*vanjski razmak od drugih elemenata*/
  min-width: 45%; /*širina elementa*/
  padding: 25px; /*unatnji razmak */
  text-decoration: none;
  color: white;
  border: 3px solid rgb(0, 0, 0);
  border-radius: 10px;
}

.r_link {
  text-decoration: none;
  color: white;
}

.parent {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
