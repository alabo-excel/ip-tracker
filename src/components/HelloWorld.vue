<template>
  <div class="hello">
    <img src="../assets/pattern-bg.png" alt="" />
    <div id="top">
      <h3>Ip Address Tracker</h3>
      <input
        v-model="ip"
        @blur="locationCheck"
        type="text"
        placeholder="Search for any Ip address or domain"
      />
    </div>
    <div id="second" v-if="loca != null" class="d-flex justify-content-center p-3">
      <div class="mx-5 text-left">
        <p>IP ADDRESS</p>
        <h6>{{ loca.ip }}</h6>
      </div>
      <div class="mx-5 text-left">
        <p>LOCATION</p>
        <h6>{{ loca.location.city }}, {{ loca.location.country }}</h6>
        <h6>{{ loca.location.postalCode }}</h6>
      </div>
      <div class="mx-5 text-left">
        <p>TIMEZONE</p>
        <h6>{{ loca.location.timezone }}</h6>
      </div>
    </div>
    <div v-else></div>
    <div>
      <GmapMap
        :center="{ lat: 4.8156, lng: 7.0498 }"
        :zoom="8"
        map-type-id="hybrid"
        style="width: 100%; height: 420px"
      >
      </GmapMap>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      map: null,
      ip: "8.8.8.1",
      loca: null,
    };
  },
  mounted() {
    // fetch("https://streetviewpublish.googleapis.com")
    // .then((response) => response.json())
    // .then((data) => console.log(data));
  },
  methods: {
    locationCheck() {
      fetch(
        "https://geo.ipify.org/api/v1?apiKey=at_ppjjelGVj8AFNAlpiiNpkFUWi0w0G&ipAddress=" +
          this.ip +
          ""
      )
        .then((response) => response.json())
        .then((data) => {
          this.loca = data;
          console.log(this.loca);
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
img {
  width: 100%;
}
input {
  padding: 10px;
  border: 0px;
  border-radius: 10px;
  width: 500px;
}
#top {
  position: absolute;
  top: 60px;
  left: 33%;
  right: auto;
}
#mapid {
  height: 180px;
}
#second{
  position: absolute;
  top: 160px;
  background-color: white;
  z-index: 1000;
  border-radius: 20px;
  left: 25%;
}
</style>
