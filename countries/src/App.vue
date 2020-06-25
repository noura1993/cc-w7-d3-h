<template>
  <div id="app">
    <div id="drop-list">
      <h1>The World</h1>
      <label for="country_select"></label>
      <select id="country_select" v-model="selectedCountry">
        <option v-for="country in countries" :value="country">{{country.name}}</option>
      </select>
    </div>
    <div class="search-container"> 
        <input class="search" type="text" placeholder="Search.." name="search" v-model="searchCountry"/>
    </div>
    <country-detail :country="selectedCountry" :searchCountry="updateSelectedCountry"></country-detail>
  </div>
</template>

<script>
import CountryList from "./components/CountryList.vue";
import CountryDetail from "./components/CountryDetail.vue";
import { eventBus } from "./main.js";

export default {
  name: "App",
  data() {
    return {
      countries: [],
      selectedCountry: null,
      searchCountry: ""
    };
  },
  computed: {
    updateSelectedCountry: function () {
      if (this.searchCountry == "") {
        return;
      }
      this.selectedCountry = this.countries.find(country => country.name.toUpperCase().includes(this.searchCountry.toUpperCase()));
    }
  },
  mounted() {
    fetch("https://restcountries.eu/rest/v2/all")
      .then(response => response.json())
      .then(jsonResponse => (this.countries = jsonResponse));

    eventBus.$on("country-selected", country => {
      this.selectedCountry = country;
    });
  },

  components: {
    "country-list": CountryList,
    "country-detail": CountryDetail
  }
};
</script>

<style>
body::after {
  background-image: url("./assets/world.jpg");
  background-size: cover;
  background-attachment: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  width: 100%;
  height: 100%;
  opacity: 0.5;
  z-index: -1;
  position: absolute;
  content: "";
}

#app {
  text-align: center;
}

#drop-list {
  text-align: center;
  display: inline;
}

#country_select {
  width: 420px;
  padding: 0.5rem 0;
  border: 1px solid #fff;
  border-radius: 18px;
  margin-bottom: 1rem;
  text-align: center;
  font-size: 1rem;
  background-color: rgb(24, 150, 172);
  color: #fff;
}

.search {
  width: 420px;
  padding: 0.5rem 0;
  border: 1px solid #fff;
  border-radius: 18px;
  margin-bottom: 1rem;
  text-align: center;
  font-size: 1rem;
  background-color: rgb(24, 150, 172);
  color: #fff;
}

::placeholder {
  color: #fff;
  opacity: 1; /* Firefox */
}

:-ms-input-placeholder { /* Internet Explorer 10-11 */
 color: #fff;
}

::-ms-input-placeholder { /* Microsoft Edge */
 color: #fff;
}

h1 {
  color: rgb(3, 7, 6);
  font-family: cursive;
}
</style>
