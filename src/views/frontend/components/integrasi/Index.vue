<template>
  <div class="mt-10">
    <v-container>
      <v-row>
        <h3 class="display-1 font-weight-bold">Integrasi</h3>
      </v-row>
      <v-row class="mt-10 text-body-2">
        Diskominfo Provinsi Banten memfasilitasi Portal Data di kabupaten dan kota di Banten agar dapat saling terhubung satu sama lain. Masyarakat pun dengan mudah untuk mencari data terbuka milik pemerintah dalam satu portal saja.
      </v-row>
      <v-row class="mt-10 mb-5">
        <h4>Sudah Terintegrasi</h4>
      </v-row>
      <v-row>
        <v-col cols="12">
          <v-divider></v-divider>
        </v-col>
        <v-col
          cols="3"
          v-for="(item, index) in iregencies"
          :key="index"
        >
          <v-card class="">
            <div class="pl-5 pt-5">
              <v-chip
                small
                color="green"
              >Terintegrasi</v-chip>
            </div>
            <div class="pl-5 pr-5 pt-5 text-center">
              <img
                :src="item.logo"
                alt=""
                width="150"
                height="175px"
              >
            </div>
            <div class="font-weight-bold mt-2 text-center text-uppercase">
              {{ item.name }}
            </div>
            <div class="pr-5 pl-5 pb-5 pt-5">
              <v-row>
                <v-icon
                  small
                  class="mr-2"
                >mdi-file</v-icon><span class="text-caption mr-2">0</span>
                <v-icon
                  small
                  class="mr-2"
                >mdi-eye</v-icon><span class="text-caption">0</span>
              </v-row>
            </div>
            <div>
              <v-btn
                :color="theme.color"
                block
                class="white--text"
              >Cari Dataset</v-btn>
            </div>
          </v-card>
        </v-col>

      </v-row>

      <v-row class="mt-10">
        <h4>Belum Terintegrasi</h4>
      </v-row>
      <v-row class="mt-10">
        <v-col
          cols="3"
          v-for="(item , index) in bregencies"
          :key="index"
        >
          <v-card class="">
            <div class="pl-5 pt-5">
              <v-chip
                small
                color="red"
              >Belum Terintegrasi</v-chip>
            </div>
            <div class="pl-5 pr-5 pt-5 text-center">
              <img
                :src="item.logo"
                alt=""
                width="150"
                height="175px"
              >
            </div>
            <div class="font-weight-bold mt-2 text-center text-uppercase">
              {{ item.name }}
            </div>
            <div class="pr-5 pl-5 pb-5 pt-5">
              <v-row>
                <v-icon
                  small
                  class="mr-2"
                >mdi-file</v-icon><span class="text-caption mr-2">100</span>
                <v-icon
                  small
                  class="mr-2"
                >mdi-eye</v-icon><span class="text-caption">10</span>
              </v-row>
            </div>
            <div>
              <v-btn
                :color="theme.color"
                block
                class="white--text"
                @click="openPortal(item.url)"
              >Kunjungi Portal</v-btn>
            </div>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";
export default {
  name: "modul-integrasi",
  data: () => ({
    iregencies: [],
    bregencies: [],
  }),
  computed: {
    ...mapState(["device", "theme", "http"]),
  },
  mounted() {
    this.setPage({
      name: "regencies",
      crud: false,
    });
    this.fetchRegency();
  },
  computed: {
    ...mapState(["device", "theme", "info", "snackbar", "loading", "http"]),
  },
  methods: {
    ...mapActions(["setPage", "getAppInfo", "snackbarClose"]),
    fetchRegency: async function () {
      try {
        let {
          data: { idata, bdata, success, message },
        } = await this.http.get("show-regency");
        this.iregencies = idata;
        this.bregencies = bdata;
      } catch (error) {}
    },
    openTopikDetail: function (val) {
      this.$router.push({
        name: "topik-detail",
        params: {
          topic_uuid: val,
        },
      });
    },
    openPortal: function (url) {
      window.open(url, "__blank");
    },
  },
};
</script>