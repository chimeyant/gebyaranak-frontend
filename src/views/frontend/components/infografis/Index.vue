<template>
  <div class="mt-10">
    <v-container>
      <v-row>
        <h3 class="display-1 font-weight-bold">Infografis</h3>
      </v-row>
      <v-row class="mt-10 text-body-2">
        Lihat gambaran informasi data tertentu dalam bentuk grafik.
      </v-row>
      <v-row class="mt-16">
        <v-card
          outlined
          class="mb-5"
        >
          <v-card-text class="">
            <v-row>
              <v-col cols="4">
                <img
                  src="/images/visualisasi-data-banten.svg"
                  alt=""
                  srcset=""
                  width="300"
                  class="animate__animated animate__fadeInRight"
                >

              </v-col>
              <v-col cols="8">
                <span class="mt-5 text-h6 animate__animated animate__fadeInUp animate__delay-1s">
                  Tampilkan hasil Infografis Data Anda di Open Data Banten!
                  Infografis Data terpilih akan dipublikasikan untuk dapat diakses oleh pengguna Open Data Banten
                </span>

                <v-row class="mt-3 animate__animated animate__fadeInUp animate__delay-1s">
                  <v-btn
                    text
                    color="indigo"
                    class="animate__animated animate__flash animate__delay-2s"
                  >Jelajahi Selengkapnya</v-btn>
                </v-row>
              </v-col>
            </v-row>

          </v-card-text>
        </v-card>
        <v-row class="pa-1">
          <v-col cols="12">
            <v-text-field
              outlined
              placeholder="Pencarian visualisasi"
              append-icon="search"
              color="orange"
            ></v-text-field>
          </v-col>
          <v-col cols="12">
            <v-row class="pl-3 pr-3 pt-5">
              <span class="text-body-2 font-weight-medium">
                {{ datas.meta.total }} Data Infografis
              </span>
              <v-spacer>
              </v-spacer>
              <v-select
                label="Urutkan"
                outlined
                dense
                style="max-width: 300px;"
                v-model="record.sorting"
                :items="sortings"
              ></v-select>
            </v-row>
          </v-col>
          <v-col cols=12>
            <div>
              <v-divider></v-divider>
              <v-row class="mt-5 justify-around">
                <v-col
                  cols="3"
                  v-for="(item, index) in datas.data"
                  :key="index"
                >
                  <v-card @click="openInfografisDetail(item.id)">
                    <img
                      :src="item.thumbnail"
                      alt=""
                      srcset=""
                      width="100%"
                    >
                    <v-card-text>
                      <span class="font-weight-bold ">
                        {{ item.title }}
                      </span>
                      <div class="mt-5">
                        <v-row>
                          <v-col cols="1">
                            <v-icon small>mdi-office-building-outline</v-icon>
                          </v-col>
                          <v-col cols="10">
                            <span>
                              {{ item.opd }}
                            </span>
                          </v-col>
                        </v-row>
                        <v-row>
                          <v-col cols="1">
                            <v-icon small>mdi-book</v-icon>
                          </v-col>
                          <v-col cols="10">
                            <span>
                              {{ item.topik }}
                            </span>
                          </v-col>
                        </v-row>

                        <v-row>
                          <v-col cols="1">
                            <v-icon small>mdi-eye</v-icon>
                          </v-col>
                          <v-col cols="10">
                            <span>
                              40
                            </span>
                          </v-col>
                        </v-row>
                      </div>
                    </v-card-text>
                  </v-card>
                </v-col>
              </v-row>

              <v-row class="justify-end">
                <div class="mt-4 mb-5">
                  <v-select
                    label="Per Halaman"
                    outlined
                    dense
                    v-model="record.itemsPerPage"
                    :items="pagination.itemsPerPage"
                  ></v-select>
                </div>
                <v-spacer></v-spacer>
                <div class="mt-4 mb-5">
                  <v-pagination
                    color="indigo"
                    v-model="pagination.page"
                    :length="datas.meta.last_page"
                  ></v-pagination>
                </div>
              </v-row>
            </div>
          </v-col>
        </v-row>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";

export default {
  name: "modul-visualisasi",
  data: () => ({
    pagination: {
      page: 1,
      itemsPerPage: [
        { text: "5", value: 5 },
        { text: "10", value: 10 },
        { text: "20", value: 20 },
      ],
    },
    datas: [],
    record: {},
    sortings: [
      { text: "Terbaru", value: "terbaru" },
      { text: "Terlama", value: "terlama" },
    ],
  }),
  computed: {
    ...mapState(["device", "theme", "http"]),
  },
  mounted() {
    this.setPage({
      name: "visualisasi",
      crud: false,
    });
    this.fetchVisualisasi();
  },
  computed: {
    ...mapState(["device", "theme", "info", "snackbar", "loading", "http"]),
  },
  methods: {
    ...mapActions(["setPage", "getAppInfo", "snackbarClose"]),
    fetchVisualisasi: async function () {
      try {
        let { data } = await this.http.get("katalog/infografis");
        this.datas = data;
        this.perPage = "10";
      } catch (error) {}
    },
    openInfografisDetail: async function (val) {
      this.$router.push({
        name: "infografis-detail",
        params: {
          infographic_uuid: val,
        },
      });
    },
  },
};
</script>