<template lang="html">
  <div class="country-detail" v-if='country !== null'>
    <h3>{{country.name}}</h3>
    <p>Capital: {{country.capital}}</p>
    <p>Population: {{country.population}}</p>
    <p>Languages: {{country.languages.map(language => language.name).join(", ")}}</p>
    <img class="flag" :src="country.flag" alt="Country Flag">
</div>
</template>

<script>
export default {
    name: "country-detail",
    props: ["country"]
}
</script>

<style>

.country-detail {
    font-size: 25px;
    background-color: #fff;
    opacity: 0.8;
    width: 40%;
    margin: auto;
    margin-top: 5%;;
    padding: 1%;
}

.flag {
    width: 15%;
}

</style>