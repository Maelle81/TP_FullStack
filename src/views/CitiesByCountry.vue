<template>
  <div class="">
    <h2>Les villes par pays</h2>
    <div>
      <div class="col">
        <label id="countries" for="countries">Pays:</label>
            <select id="country-selector" @input="fetchCities">
              <option selected disabled hidden>Choisissez un pays</option>
              <option
                v-for="country in data.allCountries"
                :key="country.id"
                :value="country._links.cities.href"
              >
                {{ country.name }}
              </option>
            </select>                 
      </div>
      <div>
        <CityCountryList v-bind:cities="data.allCities" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive, onMounted } from "vue";
// @ is an alias to /src
import CityCountryList from "@/components/CityCountryList.vue";

        const data = reactive({
          allCountries: [],
          allCities: [],          
        });

        function refresh() {
          fetch("api/countries")
              .then((response) => {
                if (!response.ok) { // status != 2XX
                  throw new Error(response.status);
                }
                 return response.json();
              })
              .then((json) => {
                data.allCountries = json._embedded.countries;
              })
              .catch((error) => alert(error));
        }

        function fetchCities() {
            fetch(document.getElementById("country-selector").value)
            .then((response) => response.json())
            .then((json) => {
              data.allCities =[];
              let listCities = json._embedded.cities;
              for(let i=0; i<listCities.length;i++){
                data.allCities.push(listCities[i])
              }
            })
            .catch((error) => alert(error));
        }      
        
        onMounted(() => {
          refresh();
          fetchCities(); // On récupère les villes (pour la table)
          
        });

</script>

