<template>
  <div>
    <navbar></navbar>
    <div class="row">
      <div class="col-12">
        <div class="position-relative overflow-hidden p-3 p-md-5 m-md-3  bg-light">
          <div class="col-md-5 p-lg-5 mx-auto my-5">
            <h1 class="display-3 font-weight-normal mb-5">{{country.name}}</h1>
                <pre>{{formatJson(country)}}</pre>

          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import navbar from "@/components/country/navbar";

import axios from "axios";

export default {
  components: {
    navbar
  },
  methods: {
    formatNumber(value) {
      return value.toLocaleString();
    },
    formatJson(obj){
        return JSON.stringify(obj, undefined, 2);
    }
  },
  asyncData({ params, error }) {
    return axios
      .get("https://restcountries.eu/rest/v2/alpha/" + params.alpha3code)
      .then(res => {
        return {
          country: res.data
        };
      })
      .catch(e => {
        console.log(e);
      });
  }
};
</script>

<style>
</style>
