<template>
  <div>
    <navbar></navbar>
    <!-- Country definition -->
    <div class="pricing-header px-3 py-3 pt-md-5 pb-md-4 mx-auto text-center">
      <h1 class="display-4">Country</h1>
      <p
        class="lead"
      >A country is a region that is identified as a distinct entity in political geography. A country may be an independent sovereign state or part of a larger state,[1] as a non-sovereign or formerly sovereign political division, or a geographic region associated with sets of previously independent or differently associated people with distinct political characteristics. Regardless of the physical geography, in the modern internationally accepted legal definition as defined by the League of Nations in 1937 and reaffirmed by the United Nations in 1945, a resident of a country is subject to the independent exercise of legal jurisdiction. There is no hard and fast definition of what regions are countries and which are not.</p>
    </div>
    <!-- Country list -->
    <div class="container">
      <div class="card-deck mb-3 text-center">
        <div class="card mb-4 shadow-sm" v-for="country in countries" :key="country.alpha3Code">
          <div class="card-header">
            <h4 class="my-0 font-weight-normal">{{country.name}}</h4>
          </div>
          <div class="card-body">
            <h1 class="card-title pricing-card-title">
              $0
              <small class="text-muted">/ mo</small>
            </h1>
            <ul class="list-unstyled mt-3 mb-4">
              <li>10 users included</li>
              <li>2 GB of storage</li>
              <li>Email support</li>
              <li>Help center access</li>
            </ul>
            <button type="button" class="btn btn-lg btn-block btn-primary">Sign up for free</button>
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
  asyncData({ params, error }) {
    return axios
      .get(`https://restcountries.eu/rest/v2/all`)
      .then(res => {
        return {
          countries: res.data
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
