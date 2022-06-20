<template>
  <div class="container-fluid p-0">
    <nav class="navbar bg-dark navbar-expand-lg bg-light">
      <div class="container-fluid">
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNavDropdown"
          aria-controls="navbarNavDropdown"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNavDropdown">
          <ul class="navbar-nav">
            <li class="nav-item">
              <a class="nav-link text-secondary" aria-current="page" href="#"
                >Home</a
              >
            </li>
            <li class="nav-item">
              <a class="nav-link text-secondary" href="#">Toevoegen</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <h1>{{ header }}</h1>
    <div class="row">
      <div class="col-6">
        <ul class="list-group">
          <li
            class="list-group-item"
            @click="selectCountry(index)"
            v-for="(country, index) in countryData.countries"
            v-bind:key="country.id"
          >
            <span v-bind:id="country.id" v-bind:title="country.details">
              {{ country.id }} -    
              {{ country.name }}
            </span>
          </li>
        </ul>
        <hr />
      </div>
      <div class="col-6">
        <h2>Selected:</h2>
        <ul class="list-group">
            <li class="list-group-item"><img :src="selectedCountry.img" class="img-fluid"></li>
          <li class="list-group-item">{{ selectedCountry.id }}</li>
          <li class="list-group-item">{{ selectedCountry.name }}</li>
          <li class="list-group-item">{{ selectedCountry.capital }}</li>
              <li class="list-group-item">{{ selectedCountry.cost }}</li>
          <li class="list-group-item">{{ selectedCountry.details }}</li>
          <li class="list-group-item" v-if="isExpensive">
            <span class="badge badge-danger badge-pill">Expensive!</span>
          </li>
          <li class="list-group-item" v-if="isOnSale">
            <span class="badge badge-warning badge-pill">On Sale!</span>
          </li>
        </ul>
      </div>
    </div>
  </div>



<button v-on:click="increment(1)" class="btn btn-success">+</button>
<button v-on:click="decrement(-1)" class="btn btn-danger">-</button>

<h3>Teller {{counter}}</h3>
</template>

<script>
import countryData from "./countryData";
  
export default {
  name: "VacationPicker",
  data() {
    return {
      countryData,
      header: "Vue Vacation Picker",
      selectedCountryIndex: 0,
      counter: 0
    };
  },
  methods: {
    increment() {
        this.counter++
    },
    decrement() {
        this.counter--
    },


    selectCountry(index) {
      this.selectedCountryIndex = index;
    },
  },
  computed: {
    selectedCountry() {
      return {
        ...this.countryData.countries[this.selectedCountryIndex],
      };
    },
    isExpensive() {
      return countryData.countries[this.selectedCountryIndex].cost > 4000;
    },

    isOnSale() {
      return countryData.countries[this.selectedCountryIndex].cost < 1000;
    },
  },
};
</script>

<style></style>
