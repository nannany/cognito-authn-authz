<template>
  <v-layout>
    <v-flex text-xs-center>
        <v-text-field v-model="name" label="name" type="text"></v-text-field>
        <v-text-field
          v-model="password"
          label="パスワード"
          type="password"
        ></v-text-field>
      <v-btn class="primary" dark @click.stop="login()">ログイン</v-btn>
    </v-flex>
  </v-layout>
</template>

<script lang="ts">
import Amplify from 'aws-amplify';
Amplify.configure({
    Auth: {
        identityPoolId: '',
        region: '',
        userPoolId: '',
        userPoolWebClientId: ''
    }
})
</script>
