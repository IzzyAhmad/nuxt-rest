<template>
    <div>
        <navbar></navbar>
        <div class="row">
            <div class="col-12">
                <img src="" alt="">
                <p>{{country}}</p>
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
  },
  asyncData({ params, error }) {
    return axios
      .get('https://restcountries.eu/rest/v2/alpha/'+params.alpha3code)
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
