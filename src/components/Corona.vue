<template>
  <div class="section">
    <b-field>
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
      <b-button type="is-primary">Search</b-button>
    </b-field>
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
              <p class="title">Confirmed</p>
              <p class="subtitle is-2">{{statewises.confirmed}}</p>
            </div>
          </b-field>
        </div>
        <div class="column">
          <b-field>
            <div class="box notification is-danger has-text-centered">
              <p class="title">Death</p>
              <p class="subtitle is-2">{{statewises.deaths}}</p>
            </div>
          </b-field>
        </div>
        <div class="column">
          <b-field>
            <div class="box notification is-success has-text-centered">
              <p class="title">Recovered</p>
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
      data: ["Karnatka", "Maharastra", "Kerala"],
      name: "",
      selected: null,
      statewises: null
    };
  },
  created() {
    axios
      .get(`https://api.covid19india.org/data.json`)
      .then(response => {
        // JSON responses are automatically parsed.
        // console.log(response.data.statewise[0].active);
        console.log(response.data);
        this.statewises = response.data.statewise[0];
        // this.posts = response.data;
      })
      .catch(e => {
        // this.errors.push(e);
        console.log(e);
      });
  },
  computed: {
    filteredDataArray() {
      return this.data.filter(option => {
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