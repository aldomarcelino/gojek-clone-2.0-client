<script>
import VueGoogleAutocomplete from "vue-google-autocomplete";
import { mapActions } from "pinia";
import { useFoodStore } from "../stores/food";

export default {
  components: { VueGoogleAutocomplete },
  data: function () {
    return {
      address: "",
      place: "",
    };
  },
  methods: {
    ...mapActions(useFoodStore, ["getRestaurantData"]),
    getRestaurant() {
      this.getRestaurantData(this.place);
    },
    getAddressData: function (addressData) {
      this.address = addressData;
      this.getRestaurantData(this.address.route);
    },
  },
  computed: {},
  mounted() {
    this.$refs.address.focus();
  },
};
</script>

<template>
  <div class="max-w-7xl mx-auto">
    <div
      class="relative flex items-center w-full h-12 rounded-lg focus-within:shadow-lg bg-black overflow-hidden mt-5 shadow-md"
      @submit.prevent="getRestaurant"
    >
      <div class="grid place-items-center h-full w-12 text-gray-300">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-6 w-6"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
          />
        </svg>
      </div>
      <vue-google-autocomplete
        ref="address"
        id="map"
        class="form-control peer h-full w-full outline-none text-gray-700 pr-2 hadow focus:outline-none focus:shadow-lg focus:shadow-slate-500 duration-100 shadow-gray-600"
        placeholder=" Search for restaurant or cuisine"
        v-on:placechanged="getAddressData"
      >
      </vue-google-autocomplete>
    </div>
  </div>
</template>
