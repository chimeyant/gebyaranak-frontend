<template>
  <div class="mt-10">
    <v-row class="grey lighten-5">
      <v-container>
        <v-row class="mt-2 ">
          <v-col cols="12">
            <v-text-field
              outlined
              placeholder="Pencarian data"
              append-icon="search"
              color="orange"
            ></v-text-field>
          </v-col>

        </v-row>
      </v-container>

    </v-row>
    <v-container>
      <v-row class="mt-5">
        <v-col cols="12">
          <span class="font-weight-bold text-uppercase">
            {{ datas.organization }}
          </span>
        </v-col>
        <v-col cols="12">
          <v-row class="pl-3 pr-3 pt-5">
            <span class="text-body-2 font-weight-medium">
              {{ datas.meta.total }} Data Ditemukan
            </span>
            <v-spacer>
            </v-spacer>
            <v-select
              label="Urutkan"
              outlined
              dense
              v-model="urutan"
              :items="urutans"
              style="max-width: 300px;"
            ></v-select>
          </v-row>
        </v-col>
        <v-divider></v-divider>
        <v-col cols=12>
          <div>
            <v-divider></v-divider>
            <v-list three-line>
              <template v-for="(item, index) in datas.data">
                <v-subheader
                  v-if="item.header"
                  :key="item.header"
                  v-text="item.header"
                ></v-subheader>

                <v-divider
                  v-else-if="item.divider"
                  :key="index"
                  :inset="item.inset"
                ></v-divider>

                <v-list-item
                  v-else
                  :key="item.title"
                >
                  <img
                    :src="item.icon"
                    alt=""
                    srcset=""
                    width="100"
                    class="mr-2 mb-2"
                    style="border-radius: 10px;"
                  >
                  <v-list-item-content class="mr-5 mt-5">
                    <v-row>
                      <v-col cols="10">
                        <div class="text-body-1">
                          {{ item.title }}
                        </div>
                      </v-col>
                      <v-col
                        cols="2"
                        class="text-center pt-10"
                      >
                        <v-btn
                          outlined
                          small
                          color="indigo"
                          @click="openData(item.tablename, item.ref_uuid)"
                        >
                          <v-icon
                            class="mr-1"
                            small
                          > mdi-eye</v-icon> Lihat
                        </v-btn>
                      </v-col>
                    </v-row>
                    <div>
                      <v-row class="pl-3 text-body-2">
                        <v-icon
                          class="mr-2"
                          small
                        >mdi-office-building-outline</v-icon><span class="mr-2">{{ item.opd }}</span>
                        <v-icon
                          class="mr-2"
                          small
                        >mdi-map</v-icon><span class="mr-2">Provinsi Banten</span>
                      </v-row>
                      <v-row class="mt-5 pl-3 text-body-2">
                        <v-icon
                          class="mr-2"
                          small
                        >mdi-calendar</v-icon><span class="mr-2">2022-2023</span>
                        <v-icon
                          class="mr-2"
                          small
                        >mdi-book</v-icon><span class="mr-2">{{ item.topik }}</span>
                        <v-icon
                          class="mr-2"
                          small
                        >mdi-clock-check</v-icon><span class="mr-2">{{ item.dataage }}</span>
                      </v-row>

                    </div>
                    <div>
                      <v-row class="mt-5 ml-5">
                        <v-chip
                          small
                          color="orange"
                          class="white--text"
                        >{{ item.tablename }}</v-chip>
                      </v-row>
                    </div>
                    <div></div>
                  </v-list-item-content>
                  <v-list-item-action>
                    <div>
                      <v-icon
                        small
                        class="mr-2"
                      >mdi-eye</v-icon><span class="text-body-2">10</span>
                    </div>
                  </v-list-item-action>
                </v-list-item>
              </template>
            </v-list>

            <v-row class="justify-end mt-10">
              <div class="mt-4 mb-5">
                <v-select
                  label="Per Halaman"
                  outlined
                  dense
                  v-model="perPage"
                  :items="perPages"
                ></v-select>
              </div>
              <v-spacer></v-spacer>
              <div class="mt-4 mb-5">
                <v-pagination
                  color="indigo"
                  v-model="page"
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
  name: "topik-detail",
  data: () => ({
    urutans: [
      { text: "AZ", value: "az" },
      { text: "ZA", value: "za" },
      { text: "Terbaru", value: "terbaru" },
      { text: "Terlama", value: "terlama" },
    ],
    perPages: [
      { text: "5", value: "5" },
      { text: "10", value: "10" },
      { text: "25", value: "25" },
    ],
    page: 1,
    datas: [],
    organization: null,
  }),
  computed: {
    ...mapState(["device", "theme", "http"]),
  },
  mounted() {
    this.setPage({
      name: "topik",
      crud: false,
    });
    this.fetchDataset();
  },
  computed: {
    ...mapState(["device", "theme", "info", "snackbar", "loading", "http"]),
  },
  methods: {
    ...mapActions(["setPage", "getAppInfo", "snackbarClose"]),
    fetchDataset: async function () {
      try {
        let { data } = await this.http.get(
          "katalog/produsen-data/" + this.$route.params.organization_uuid
        );
        this.datas = data;
        this.perPage = "10";
      } catch (error) {}
    },
    openData: function (tablename, refuuid) {
      if (tablename == "dataset") {
        this.$router.push({
          name: "dataset-detail",
          params: {
            dataset_uuid: refuuid,
          },
        });
      }
      if (tablename == "visualisasi") {
        this.$router.push({
          name: "visualisasi-detail",
          params: {
            visualization_uuid: refuuid,
          },
        });
      }
      if (tablename == "infografik") {
        this.$router.push({
          name: "infografis-detail",
          params: {
            infographic_uuid: refuuid,
          },
        });
      }

      if (tablename == "videografis") {
        this.$router.push({
          name: "videografis",
        });
      }

      if (tablename == "document") {
        this.$router.push({
          name: "dokumen",
        });
      }
    },
  },
};
</script>