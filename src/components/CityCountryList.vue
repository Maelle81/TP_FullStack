<template>
    
    <!--<p>coucou</p>
    <div class="form-group">
        <label v-for="country in data.countries" :key="country.id">Pays :</label>
        <select class ="form-control" @click="$emit('eventCity', country.name)">
            <option disabled="" value="">Choisissez un pays</option>
            <option v-model="name">{{country.name}}</option> 
        </select>       
    </div>
    <div id="cities">
        <table>
            <tr><th>Nom</th><th>Population (en millions)</th></tr>
            <tr><td>{{city.nom}}</td><td>{{city.population}}</td></tr>
        </table>
    </div>  -->
    
    <div>
    <table class="table table-bordered table-sm table-hover">
      <thead>
        <tr>
          <th>Nom</th>
          <th>Population</th>          
        </tr>
      </thead>
      <tbody>
        <tr v-for="city in cities" :key="city.id">
          <td>{{ city.name }}</td>
          <td>{{ city.population }}</td>
        </tr>
      </tbody>
    </table>
  </div>

   
</template>

<script setup>
    const props = defineProps({
  cities: {
    type: Array,
    required: true,
  },
});
</script>


