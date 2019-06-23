<template>
  <div class="container">
    <div class="flex xs12 sm8 offset-sm2">
      <v-alert v-model="show_error" v-bind="error" type="warning" icon="info">{{ error }}</v-alert>
    </div>
    <v-card color="blue-grey lighten-4" class="white--text">
      <v-card-title>
        <h2>Cognitoによる認証・認可</h2>
      </v-card-title>
      <v-card-actions>
        <v-layout align-center>
          <v-btn class="primary" @click.stop="hello()">Hello!</v-btn>
          <v-spacer/>
          <v-btn class="orange" @click.stop="goodbye()">Goodbye!</v-btn>
        </v-layout>
      </v-card-actions>
      <v-card-text>
        <p class="text-lg-right" v-model="show_result" v-bind="response">{{ response }}</p>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
import axios from "axios";

export default {
  layout: "initial",
  data() {
    return {
      show_error: false,
      show_result: false,
      error: "",
      token: this.$route.hash.split(/[=&]/)[1],
      response: ""
    };
  },
  methods: {
    hello() {
      axios
        .get("http://localhost:8080/hello", {
          headers: { Authorization: "Bearer " + this.token },
          data: {}
        })
        .then(response => {
          this.show_result = true;
          this.show_error = false;
          this.response = response.data;
        })
        .catch(error => {
          this.show_result = false;
          this.show_error = true;
          this.error = this.error;
          this.response = "";
        });
    },
    goodbye() {
      axios
        .get("http://localhost:8080/goodbye", {
          headers: { Authorization: "Bearer " + this.token },
          data: {}
        })
        .then(response => {
          this.show_result = true;
          this.show_error = false;
          this.response = response.data;
        })
        .catch(error => {
          this.show_result = false;
          this.show_error = true;
          this.error = error;
          this.response = "";
        });
    }
  }
};
</script>
