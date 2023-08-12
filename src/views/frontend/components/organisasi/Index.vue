<template>
  <div class="mt-10">
    <v-container>
      <v-row>
        <h3 class="display-1 font-weight-bold">Produsen Data</h3>
      </v-row>
      <v-row class="mt-10 text-body-2">
        <v-col cols="12">
          Di halaman ini tersedia daftar Produsen Data yang berkontribusi untuk membangun ekosistem data yang terbuka dan terpercaya melalui publikasi data di Open Data Banten.
        </v-col>
      </v-row>
      <v-row class="mt-5">
        <v-col cols="12">
          <v-text-field
            outlined
            prepend-inner-icon="search"
            placeholder="Cari Organisasi"
            color="orange"
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row class="pa-2">
        <div>
          <span class="text-body-2 font-weight-medium">
            {{ meta.total }} Produsen Data
          </span>
        </div>
        <v-spacer></v-spacer>
        <div>
          <v-select
            placeholder="Urutkan"
            outlined
            dense
            :items="urutans"
          ></v-select>
        </div>
      </v-row>
      <v-row class="pa-2 mb-5">
        <v-divider></v-divider>
      </v-row>
      <v-row class="animate__animated animate__fadeInUp">
        <v-col
          cols="2"
          v-for="item in datas"
          :key="item.id"
        >
          <v-card
            class="pa-2"
            height="250"
            @click="openProdusenDataDetail(item.id)"
          >
            <div class="text-center">
              <img
                src="/images/logo-banten.png"
                alt=""
                width="100"
              >
            </div>
            <div class="text-body-2 font-weight-medium mt-5">
              {{ item.name }}
            </div>
            <div class="mt-2">
              <v-icon
                small
                class="mr-2"
              >mdi-file</v-icon><span class="text-caption font-weight-thin mr-2">50</span>
              <v-icon
                small
                class="mr-2"
              >mdi-chart-histogram</v-icon><span class="text-caption font-weight-thin">0</span>
            </div>
          </v-card>
        </v-col>

      </v-row>
      <v-row class="justify-end pa-2">
        <div class="mt-4 mb-5">
          <v-select
            label="Per Halaman"
            outlined
            dense
            :items="perHalamans"
          ></v-select>
        </div>
        <v-spacer></v-spacer>
        <div class="mt-4 mb-5">
          <v-pagination
            color="indigo"
            v-model="page"
            :length="meta.last_page"
          ></v-pagination>
        </div>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";
export default {
  name: "modul-organisasi",
  data: () => ({
    page: 1,
    urutans: [
      { text: "A-Z", value: "a-z" },
      { text: "Z-A", value: "z-a" },
    ],
    perHalamans: [
      { text: "10", value: 10 },
      { text: "25", value: 25 },
      { text: "50", value: 50 },
    ],
    datas: [],
    meta: {},
  }),
  computed: {
    ...mapState(["device", "theme", "http"]),
  },
  mounted() {
    this.setPage({
      name: "topik",
      crud: false,
    });
    this.fetchProdusenData();
  },
  computed: {
    ...mapState(["device", "theme", "info", "snackbar", "loading", "http"]),
  },
  methods: {
    ...mapActions(["setPage", "getAppInfo", "snackbarClose"]),
    fetchProdusenData: async function () {
      try {
        let {
          data: { success, code, errors, message, data, meta },
        } = await this.http.get("show-produsen-data");
        this.datas = data;
        this.meta = meta;
      } catch (error) {}
    },
    openProdusenDataDetail: function (val) {
      this.$router.push({
        name: "organisasi-details",
        params: {
          organization_uuid: val,
        },
      });
    },
  },
};
</script>