<template>
  <div class="mt-10">
    <v-container>
      <v-row>
        <v-col cols=12>
          <span class="text-h4">
            {{ record.name }}
          </span>
          <v-row class="mt-3 ml-2 mr-2">
            <div class="mr-2">
              <v-icon class="mr-2">mdi-calendar</v-icon> <span class="text-body-2">28 February 2023</span>
            </div>
            <div class="mr-2">
              <v-icon class="mr-2">mdi-eye</v-icon> <span class="text-body-2">0</span>
            </div>
            <v-spacer></v-spacer>
            <span class="text-body-2 grey--text mr-2">Bagikan :</span>
            <v-icon
              color="blue"
              class="mr-2"
            >mdi-facebook</v-icon>
            <v-icon
              color="blue"
              class="mr-2"
            >mdi-twitter</v-icon>
            <v-icon
              color="grenn"
              class="mr-2"
            >mdi-whatsapp</v-icon>
          </v-row>
        </v-col>
        <v-col cols="12">
          <v-card outlined>
            <v-card-text>
              <v-img
                :src="record.thumbnail"
                alt=""
                srcset=""
              />
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";
export default {
  name: "detail-visualisasi",
  data: () => ({
    record: {},
  }),
  computed: {
    ...mapState(["page", "device", "theme"]),
  },
  mounted() {
    this.setPage({
      name: "visualisasi",
      crud: false,
    });
    this.fetchtData();
  },
  computed: {
    ...mapState(["device", "theme", "info", "snackbar", "loading", "http"]),
  },
  methods: {
    ...mapActions(["setPage", "getAppInfo", "snackbarClose"]),
    fetchDataset: async function () {
      try {
        let {
          data: { data },
        } = await this.http.get(
          "show-dataset/" + this.$route.params.dataset_uuid
        );
        this.record = data;
        this.headers = data.headers;
        this.perPage = "10";
      } catch (error) {}
    },
    fetchtData: async function () {
      try {
        let {
          data: { success, code, message, data },
        } = await this.http.get(
          "show-visualisasi/" + this.$route.params.visualization_uuid
        );
        this.record = data;
      } catch (error) {}
    },
  },
};
</script>