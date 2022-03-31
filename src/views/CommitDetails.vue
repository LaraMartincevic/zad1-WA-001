<template>
  <div class="parent">
    <div class="commit">
      <h1>Detalji Commita</h1>
     
        <li>Ime autora: {{ commit.commit.author.name }}</li>
        <li>Email adresa: {{ commit.commit.author.email }}</li>
        <li>Poruka commita: {{ commit.commit.message }}</li>
        <li>Datum: {{ commit.commit.author.date }}</li>
   
    </div>
  </div>
</template>

<script>
export default {
  name: "CommitDetails",
  props: {
    sha: String,
  },

  data() {
    return {
      commit: [],
    };
  },

  created: async function () {
    let get_request = await fetch(
      "https://api.github.com/repos/vuejs/vue/commits/" + this.sha
    );
    let response = await get_request.json();
    this.commit = response;
    console.log(get_request);
  },
};
</script>

<style scoped>
.commit {
  text-align: left;
 width: 30rem;
  background-color: yellow;
  list-style-type: none;
  padding: 30px;
  display: flex;
  flex-direction: column;
  

}

li{margin-top:5px ;
margin-bottom: 5px;}

.parent {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

h1 {
  margin-bottom: 20px;
}
</style>