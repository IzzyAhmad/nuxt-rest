<template>
  <div >
    <navbar></navbar>
    <!-- Country definition -->
    <div class="pricing-header px-3 py-3 pt-md-5 pb-md-4 mx-auto text-center">
      <h1 class="display-4" style="font-family: 'Lato', sans-serif;">Country</h1>
      <p
        class="lead"
      >A country is a region that is identified as a distinct entity in political geography. A country may be an independent sovereign state or part of a larger state,[1] as a non-sovereign or formerly sovereign political division, or a geographic region associated with sets of previously independent or differently associated people with distinct political characteristics. Regardless of the physical geography, in the modern internationally accepted legal definition as defined by the League of Nations in 1937 and reaffirmed by the United Nations in 1945, a resident of a country is subject to the independent exercise of legal jurisdiction. There is no hard and fast definition of what regions are countries and which are not.</p>
    </div>
    <!-- Country list -->
    <div class="row mb-2 px-3 py-3 mx-auto">
      <div class="col-md-4" v-for="country in countries" :key="country.alpha3Code">
        <div
          class="row no-gutters border rounded overflow-hidden flex-md-row mb-4 shadow-sm h-md-250 position-relative"
        >
          <div class="col p-4 d-flex flex-column position-static">
            <strong class="d-inline-block mb-2 text-primary">{{country.region}}</strong>
            <h3 class="mb-0">{{country.name}}</h3>
            <div class="mb-1 text-muted">Populations: {{formatNumber(country.population)}}</div>
            <p class="card-text mb-auto"></p>
            <nuxt-link :to="'/country/'+country.alpha3Code" class="stretched-link">More..</nuxt-link>
          </div>
          <div class="col-auto d-none d-lg-block">
            <img
              class="bd-placeholder-img mx-auto"
              width="200"
              height="130"
              :src="country.flag"
              preserveAspectRatio="xMidYMid slice"
              focusable="false"
              style="position: relative;top: 50%;transform: translateY(-50%);"
              role="img"
              aria-label="Placeholder: Thumbnailasds"
            >
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
    wikiDeff(name) {
      const proxyurl = "https://cors-anywhere.herokuapp.com/";
      return axios
        .get(proxyurl+'https://wordsapiv1.p.mashape.com/words/'+name+'/definitions')
        .then(res => {
          return {
            wiki: res.data
          };
        })
        .catch(e => {
          console.log(e);
        });
    }
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
