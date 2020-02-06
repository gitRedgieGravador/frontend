<template>
  <div>
    <br />
    <br />
    <!-- <v-card color="info" dark outlined>
      <hr />
      <center>
        <h1>Pending Requests</h1>
      </center>
      <hr />
    </v-card>
    <v-expansion-panels inset focusable> -->
      <RequestTable
        
        :request="requests"
      :title="'Approved Requests'"
        @remove="removeItem(request)"
      />
    <!-- </v-expansion-panels> -->
  </div>
</template>
<script>
import RequestTable from "../modules/tibs/RequestTableNoButtons.vue";
import { getApproved } from "../actions/requestAxios.js";
// import io from "socket.io-client";
// var socket = io.connect("http://backendpnrms-env.dn4iumcmuw.us-east-1.elasticbeanstalk.com:3232/");
export default {
  components: {
    RequestTable
  },
  data() {
    return {
      sample: "sample",
      username: "redgie",
      requests: []
    };
  },
  methods: {
    removeItem(request) {
      this.requests.splice(this.requests.indexOf(request), 1);
    }
  },
  mounted() {
    getApproved()
      .then(data => (this.requests = data.data))
      .catch(err => alert(err));
  }
};
</script>
