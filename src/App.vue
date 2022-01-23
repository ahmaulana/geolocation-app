<template>
  <div class="flex items-center justify-center w-screen h-screen">
    <div class="bg-blue-400 p-10">
      <h1 class="text-2xl mb-5">Form</h1>
      <form class="space-y-4">
        <div>
          <label class="block mb-2">Alamat</label>
          <textarea
            class="rounded-md p-4 w-full"
            v-model="address"
          ></textarea>
        <button class="p-2 bg-gray-500 text-white text-lg rounded-lg w-full" @click.prevent="getGeo">Get Data</button>
        </div>
        <div class="flex space-x-4">
          <div class="flex flex-col">
            <label>Latitude</label>
            <input type="text" v-model="lat" readonly />
          </div>
          <div class="flex flex-col">
            <label>Longitude</label>
            <input type="text" v-model="long" readonly />
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      address: "",
      lat: "",
      long: ""
    };
  },
  methods: {
    getGeo() {
      const token = "Mwo3B7OO_00GkP2p4Xepp4VaOX0gR-_L20JK1THmha0";
      let address = this.address;
      axios
        .get(
          "https://geocode.search.hereapi.com/v1/geocode?q=" +
            address +
            "&apiKey=" +
            token
        )
        .then((response) => {
          this.lat = response.data.items[0].position.lat
          this.long = response.data.items[0].position.lng
        });
    },
  },

  // mounted() {
  //   const token = 'gXMFfOnQC37MiaRAJb3VQs5eXqOXN3kUvmL2go6FIZU'
  //   let address = "Pasar Mranggen"
  //   axios
  //     .get('https://geocode.search.hereapi.com/v1/geocode?q='+address+'&apiKey='+token)
  //     .then(response => {
  //       console.log(response)
  //     })
  // }
};
</script>

<style>
</style>
