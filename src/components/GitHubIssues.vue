<template>
  <div class="container">
    <h1>Vue.js + Github</h1>
    <p class="lead">
      Página que lista issues de um repositório do Github, usando Vue.js.
    </p>

    <div class="row">
      <div class="col">
        <div class="form-group">
          <input v-model="username" type="text" class="form-control" placeholder="github username" />
          <!-- {{ username }} -->
        </div>
      </div>

      <div class="col">
        <div class="form-group">
          <input v-model="repository" type="text" class="form-control" placeholder="github repositório" />
          <!-- {{ repository }} -->
        </div>
      </div>

      <div class="col-3">
        <div class="form-group">
          <button v-on:click.prevent.stop="getIssues()" class="btn btn-success">
            buscar
          </button>
          <button v-on:click.prevent.stop="reset()" class="btn btn-danger">
            limpar
          </button>
        </div>
      </div>
    </div>

    <br />
    <hr />
    <br />

    <table class="table table-sm table-bordered">
      <thead>
        <tr>
          <th width="100">Número</th>
          <th>Título</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="issue in issuesList" :key="issue.number">
          <td>{{ issue.number }}</td>
          <td>{{ issue.title }}</td>
        </tr>

        <tr v-if="issuesList.length == 0">
          <td class="text-center" colspan="2">Nenhuma issue encontrada!</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "GitHubIssues",
  data() {
    return {
      username: "",
      repository: "",
      issuesList: [],
    };
  },
  methods: {
    reset() {
      this.username = "";
      this.repository = "";
      this.issuesList = [];
    },
    getIssues() {
      const urlApi = `https://api.github.com/repos/${this.username}/${this.repository}/issues`;

      axios.get(urlApi).then((response) => {
        console.log(response);
        this.issuesList = response.data;
      });
    },
  },
};
</script>

<style>

</style>