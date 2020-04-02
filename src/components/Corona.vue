<template>
  <div class="section">
    <b-field class="is-spaced">
      <b-autocomplete
        rounded
        v-model="name"
        :data="filteredDataArray"
        placeholder="Search state"
        icon="magnify"
        clearable
        @select="option => selected = option"
      >
        <template slot="empty">No results found</template>
      </b-autocomplete>
      <button class="button is-primary">Search</button>
    </b-field>
    <b-field class="is-spaced has-text-danger ">
      <p class="text-danger has-text-centered">Last updated:<span class="has-text-success"> {{statewises.lastupdatedtime}}</span></p>
    </b-field>

    <!-- <div class v-for="(data,index) in statewises" :key="index">
      <div v-for="(i,j) in data.statewise" :key="j">
        <ul>
          <li v-for="(k,index) in i" :key="index">{{k.active}}</li>
        </ul>
      </div>
    </div>-->

    <div class="section">
      <div class="columns">
        <div class="column">
          <b-field>
            <div class="box notification is-primary has-text-centered">
              <p class="title is-3 is-spaced">Active</p>
              <p class="subtitle is-2">{{statewises.active}}</p>
            </div>
          </b-field>
        </div>
        <div class="column">
          <b-field>
            <div class="box notification is-warning has-text-centered">
              <p class="title is-spaced">Confirmed</p>
              <p class="subtitle is-2">{{statewises.confirmed}}</p>
            </div>
          </b-field>
        </div>
        <div class="column">
          <b-field>
            <div class="box notification is-danger has-text-centered">
              <p class="title is-spaced">Deceased</p>
              <p class="subtitle is-2">{{statewises.deaths}}</p>
            </div>
          </b-field>
        </div>
        <div class="column">
          <b-field>
            <div class="box notification is-success has-text-centered">
              <p class="title is-spaced">Recovered</p>
              <p class="subtitle is-2">{{statewises.recovered}}</p>
            </div>
          </b-field>
        </div>
      </div>
    </div>
    <!-- <p>{{statewises}}</p> -->
  </div>
</template>

<script>
import axios from "axios";

//

export default {
  data() {
    return {
      stateName: [
        "Andaman and Nicobar Islands",
        "Andhra Pradesh",
        "Arunachal Pradesh",
        "Assam",
        "Bihar",
        "Chandigarh",
        "Chhattisgarh",
        "Dadra and Nagar Haveli",
        "Daman and Diu",
        "Delhi",
        "Goa",
        "Gujarat",
        "Haryana",
        "Himachal Pradesh",
        "Jammu",
        "Jharkhand",
        "Karnataka",
        "Kashmir",
        "Kerala",
        "Ladakh",
        "Lakshadweep",
        "Madhya Pradesh",
        "Maharashtra",
        "Manipur",
        "Meghalaya",
        "Mizoram",
        "Nagaland",
        "Odisha",
        "Puducherry",
        "Punjab",
        "Rajasthan",
        "Sikkim",
        "Tamil Nadu",
        "Telangana",
        "Tripura",
        "Uttarakhand",
        "Uttar Pradesh",
        "West Bengal"
      ],
      name: "",
      selected: null,
      statewises: []
    };
  },
  created() {
    axios
      .get(`https://api.covid19india.org/data.json`)
      .then(response => {
        // console.log(response.data.statewise[0].active);
        console.log(response);
        this.statewises = response.data.statewise[0];
      })
      .catch(e => {
        console.log(e);
      });
  },
  computed: {
    filteredDataArray() {
      return this.stateName.filter(option => {
        return (
          option
            .toString()
            .toLowerCase()
            .indexOf(this.name.toLowerCase()) >= 0
        );
      });
    }
  }
};
</script>

<style>
.box {
  max-width: 100%;
}

</style>