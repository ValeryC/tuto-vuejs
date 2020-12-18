<template>
  <div id="app">
    <v-container>
      <v-layout row>
        <div>
          <v-btn v-on:click="loadApi" color="primary">Load Data</v-btn>
        </div>
      </v-layout>
    </v-container>
    <v-container>
      <v-alert v-show="dataLoaded==1" :value="true" type="success">Data loaded successfully</v-alert>
      <v-alert v-show="dataLoaded==2" :value="true" type="error">Data loaded unsuccessfully</v-alert>
    </v-container>

    <pre>
        {{$data}}
      </pre>
  </div>
</template>



<script>
export default {
  name: "Home",
  data() {
    return {
      dataLoaded: 0,
      apiData: undefined
    };
  },
  methods: {
    loadApi: function() {
      this.dataLoaded = 0;
      this.$http
        .get("https://jsonplaceholder.typicode.com/posts")
        .then(this.successCallback, this.errorCallback);
    },
    successCallback: function(response) {
      this.dataLoaded = 1;
      console.log("successCallback response:", response);
      this.apiData = response.data;
    },
    errorCallback: function(response) {
      this.dataLoaded = 2;
      console.log("errorCallback response:", response);
    }
  }
};
</script>
