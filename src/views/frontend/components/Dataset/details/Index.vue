<template>
  <div class="mt-10">
    <v-container>
      <v-row>
        <v-col cols=12>
          <v-card
            outlined
            height="200"
          >
            <v-img
              src="/images/banten.jpeg"
              height="196"
            >
              <v-col cols="12">
                <span class="font-weight-bold display-1 animate__animated animate__slideInRight">
                  {{ record.title }}
                </span>
              </v-col>

              <v-row class="mt-3">
                <v-col cols="1">
                  <img
                    src="/images/logo-banten.png"
                    alt=""
                    width="50"
                    class="ml-3 mt-2"
                  >
                </v-col>
                <v-col cols="10">
                  <div class="mb-2">
                    <span class="font-weight-bold ">{{ record.opd }}</span>
                  </div>
                  <v-row class="mt-2 ">
                    <div class="mr-3">
                      <v-icon
                        class="mr-1"
                        color="orange"
                      >mdi-book</v-icon>{{ record.topik }}
                    </div>
                    <div class="mr-3">
                      <v-icon
                        class="mr-1"
                        color="purple"
                      >mdi-calendar</v-icon>2022-2023
                    </div>
                    <div class="mr-3">
                      <v-icon
                        class="mr-1"
                        color="blue"
                      >mdi-alarm</v-icon>{{ record.dataage }}
                    </div>
                    <v-spacer></v-spacer>
                    <div class="">
                      <v-chip
                        color="green white--text"
                        small
                      >
                        <v-icon
                          class="mr-2 white--text"
                          small
                        >mdi-eye</v-icon>{{ record.counter }}
                      </v-chip>
                    </div>
                  </v-row>
                </v-col>
              </v-row>

            </v-img>
          </v-card>
        </v-col>
        <v-col cols="12">
          <v-card outlined>
            <v-card-title>
              <v-tabs
                :color="theme.color"
                v-model="tab"
              >
                <v-tab href="#data">Data</v-tab>
                <v-tab href="#meta">Metadata</v-tab>
              </v-tabs>
            </v-card-title>
            <v-card-text>
              <v-tabs-items v-model="tab">
                <v-tab-item value="data">
                  <div>
                    <span class="text-h5">Deskripsi Data</span>
                  </div>
                  <div class="text-body mt-5">

                    {{ record.description }}
                  </div>
                </v-tab-item>
                <v-tab-item value="meta">
                  <v-col cols="12">
                    <v-row>
                      <v-col cols="12">
                        <span class="text-h6">METADATA</span>
                      </v-col>
                      <v-col cols="3">
                        <span>Dataset diperbaharui</span>
                      </v-col>
                      <v-col cols="9">
                        <span>{{ record.meta.updated_at }}</span>
                      </v-col>
                      <v-col cols="3">
                        <span>Dataset dibuat</span>
                      </v-col>
                      <v-col cols="9">
                        <span>{{ record.meta.created_at }}</span>
                      </v-col>
                      <v-col cols="3">
                        <span>Pengukuran Dataset</span>
                      </v-col>
                      <v-col cols="9">
                        <span>{{ record.meta.pengukuran }}</span>
                      </v-col>
                      <v-col cols="3">
                        <span>Tingkat Penyajian Dataset</span>
                      </v-col>
                      <v-col cols="9">
                        <span>{{ record.meta.tingkat }}</span>
                      </v-col>
                      <v-col cols="3">
                        <span>Cakupan Dataset</span>
                      </v-col>
                      <v-col cols="9">
                        {{ record.meta.cakupan }}
                      </v-col>
                      <v-col cols="3">
                        <span>Produsen</span>
                      </v-col>
                      <v-col cols="9">
                        {{ record.meta.produsen }}
                      </v-col>
                      <v-col cols="3">
                        <span>Bidang</span>
                      </v-col>
                      <v-col cols="9">
                        <span>{{ record.meta.bidang }}</span>
                      </v-col>
                      <v-col cols="3">
                        <span>Penanggungjawab</span>
                      </v-col>
                      <v-col cols="9">
                        <span>{{ record.meta.penanggungjawab }}</span>
                      </v-col>
                      <v-col cols="3">
                        <span>Satuan Dataset</span>
                      </v-col>
                      <v-col cols="9">
                        <span>{{ record.meta.satuandataset }}</span>
                      </v-col>
                      <v-col cols="3">
                        <span>Dimensi Dataset</span>
                      </v-col>
                      <v-col cols="9">
                        <span>{{ record.meta.dimensi }}</span>
                      </v-col>
                      <v-col cols="3">
                        <span>Keterangan Dataset</span>
                      </v-col>
                      <v-col cols="9">
                        <span>{{ record.meta.catatan }}</span>
                      </v-col>
                    </v-row>
                  </v-col>
                </v-tab-item>
              </v-tabs-items>
            </v-card-text>
          </v-card>
        </v-col>

        <v-col cols=12>
          <v-card outlined>
            <v-row class="ml-2">
              <v-col cols="5">
                <v-tabs
                  :color="theme.color"
                  v-model="tab2"
                  background-color="grey"
                  class="white--text"
                  style="max-width:300px"
                >
                  <v-tab
                    class="white--text"
                    href="#tabel"
                  >Tabel</v-tab>
                  <v-tab
                    class="white--text"
                    href="#grafik"
                  >Grafik</v-tab>
                  <v-tab
                    class="white--text"
                    href="#map"
                  >Peta</v-tab>
                </v-tabs>
              </v-col>
              <v-col cols="7">
                <v-row class="justify-end pt-5 pr-10">
                  <v-menu offset-y>
                    <template v-slot:activator="{ on, attrs }">
                      <v-btn
                        color="primary"
                        dark
                        v-bind="attrs"
                        v-on="on"
                        v-show="tab"
                        outlined
                      >
                        Download | <v-icon class="mr-2">mdi-arrow-down-circle</v-icon>
                      </v-btn>
                    </template>
                    <v-list>
                      <v-list-item @click="postDownload(record.download_csv)">
                        <v-list-item-title>
                          <v-icon class="mr-2">mdi-file-excel</v-icon>
                          Excel File</v-list-item-title>
                      </v-list-item>
                      <v-list-item @click="postDownload(record.download_json)">
                        <v-list-item-title>
                          <v-icon class="mr-2">mdi-api</v-icon> RestApi
                        </v-list-item-title>
                      </v-list-item>
                    </v-list>
                  </v-menu>
                </v-row>
              </v-col>
            </v-row>

            <v-tabs-items v-model="tab2">
              <v-tab-item value="tabel">
                <v-col cols="12">
                  <v-card class="animated animate__fadeInUp rounded-0">
                    <v-card-title :class="`flex  ` + theme.color + ` lighten-1`">
                      <v-text-field
                        v-model="search"
                        append-icon="mdi-magnify"
                        label="Pencarian"
                        single-line
                        hide-details
                        solo
                        dense
                        :color="theme.color"
                        style="max-width: 350px"
                      ></v-text-field>
                      <v-spacer>
                      </v-spacer>
                      <v-tooltip
                        :color="theme.color"
                        bottom
                      >
                        <template v-slot:activator="{ on }">
                          <v-btn
                            text
                            small
                            icon
                            v-on="on"
                            @click="fetchDatasetData"
                          >
                            <v-icon :color="theme.mode == 'dark' ? `white` : `black`">refresh</v-icon>
                          </v-btn>
                        </template>
                        <span>Refresh Data</span>
                      </v-tooltip>
                    </v-card-title>
                    <v-data-table
                      v-show="device.desktop"
                      :headers="headers"
                      :items="records"
                      class="elevation-2 mb-1"
                      :color="theme.color"
                      loading-text="Sedang memuat data...!"
                      :search="search"
                      :loading="loading"
                      no-data-text="Tidak ada data untuk ditampilkan...!"
                    >
                      <v-progress-linear
                        slot="progress"
                        :color="theme.color"
                        height="1"
                        indeterminate
                      ></v-progress-linear>
                    </v-data-table>
                  </v-card>
                </v-col>
              </v-tab-item>
              <v-tab-item value="grafik">
                <v-row class="mt-5">
                  <v-col cols="8">
                    <bar-chat
                      :title="record.title"
                      :labels="grafik.labels"
                      :datas="grafik.datas"
                      :key="componentKey"
                      v-show="grafik.model=='bar'"
                    />
                    <pei-chart
                      :title="record.title"
                      :labels="grafik.labels"
                      :datas="grafik.datas"
                      v-show="grafik.model=='pie'"
                      :key="componentKey"
                    ></pei-chart>
                  </v-col>

                  <v-col cols="4">
                    <v-card
                      outlined
                      class="mr-5"
                    >
                      <v-card-text>
                        <v-col cols="12">
                          <div><span>Sesuaikan Tampilan Grafik</span></div>
                        </v-col>
                        <v-col cols="12">
                          <v-select
                            label="Jenis Grafik"
                            outlined
                            dense
                            hide-details
                            v-model="grafik.model"
                            :items="grafiks"
                          ></v-select>
                        </v-col>
                        <v-col cols="12">
                          <v-select
                            label="Axis X"
                            outlined
                            dense
                            hide-details
                            v-model="grafik.axisx"
                            :items="combodataset"
                          ></v-select>
                        </v-col>
                        <v-col cols="12">
                          <v-select
                            label="Axis Y"
                            outlined
                            dense
                            hide-details
                            v-model="grafik.axisy"
                            :items="combodataset"
                          ></v-select>
                        </v-col>
                        <v-col cols="12">
                          <v-select
                            label="Group Data"
                            outlined
                            dense
                            hide-details
                            v-model="grafik.groupby"
                            :items="combodataset"
                          ></v-select>
                        </v-col>
                        <v-col cols="12">
                          <v-btn
                            block
                            :color="theme.color"
                            outlined
                            @click="applyGrafik"
                          >
                            Terapkan
                          </v-btn>
                        </v-col>
                      </v-card-text>
                    </v-card>
                  </v-col>

                </v-row>
              </v-tab-item>
              <v-tab-item value="map">
                <v-row class="pa-5">
                  <v-col cols="12">
                    <l-map
                      style="height: 500px ; z-index:0 ;"
                      :zoom="zoom"
                      :center="center"
                      v-show="record.map_type !== '3'"
                    >
                      <v-geosearch
                        :options="geosearchOptions"
                        style="width:100px; border: 1px;"
                      ></v-geosearch>
                      <l-tile-layer
                        :url="url"
                        :attribution="attribution"
                      ></l-tile-layer>

                      <l-geo-json
                        :geojson="geojson"
                        :options="options"
                        :optionsStyle="geostyle"
                      ></l-geo-json>
                      <l-geo-json
                        :geojson="geojson2"
                        :options="options"
                        :optionsStyle="geostyle2"
                      ></l-geo-json>
                      <l-geo-json
                        :geojson="geojson3"
                        :options="options"
                        :optionsStyle="geostyle3"
                      ></l-geo-json>
                      <l-geo-json
                        :geojson="geojson4"
                        :options="options"
                        :optionsStyle="geostyle4"
                      ></l-geo-json>
                      <l-geo-json
                        :geojson="geojson5"
                        :options="options"
                        :optionsStyle="geostyle5"
                      ></l-geo-json>
                    </l-map>
                    <iframe
                      width="100%"
                      height="600px"
                      frameborder="0"
                      scrolling="no"
                      marginheight="0"
                      marginwidth="0"
                      title=" Peta rencana penyusunan data geospasial Base Transceiver Station (BTS) Provinsi Banten"
                      :src="record.map_url"
                    ></iframe>
                  </v-col>
                </v-row>
              </v-tab-item>
            </v-tabs-items>

          </v-card>
        </v-col>
      </v-row>

    </v-container>
  </div>
</template>
    
<script>
import { mapState, mapActions } from "vuex";
import BarChat from "../../../../backend/pages/chart/BarChart.vue";
import PeiChart from "../../../../backend/pages/chart/PieChart.vue";
import {
  LMap,
  LTileLayer,
  LMarker,
  LIcon,
  LPopup,
  LTooltip,
  LPolygon,
  LGeoJson,
} from "vue2-leaflet";
import { OpenStreetMapProvider } from "leaflet-geosearch";
import VGeosearch from "vue2-leaflet-geosearch";
import "leaflet/dist/leaflet.css";

export default {
  name: "modul-dokumen",
  components: {
    BarChat,
    PeiChart,
    LMap,
    LTileLayer,
    LMarker,
    VGeosearch,
    LIcon,
    LPopup,
    LTooltip,
    LGeoJson,
  },
  data: () => ({
    tab: null,
    tab2: null,
    headers: [],
    bodys: [],
    search: null,
    record: {},
    records: [],
    loading: false,
    grafiks: [
      { text: "Bar Chart", value: "bar" },
      { text: "Pie Chart", value: "pie" },
    ],
    jenisgrafik: null,
    axisx: null,
    axisy: null,
    groupdata: null,

    //map property
    //url: "https://{s}.tile.opentopomap.org/{z}/{x}/{y}.png",
    url: "https://tile.openstreetmap.org/{z}/{x}/{y}.png",
    attribution:
      '&copy; <a target="_blank" href="">Dinas Komunikas Informatika Statistik dan Persandian',
    zoom: 9,
    //-6.1716001, 106.6405384
    center: [-6.512449, 106.266096],

    geosearchOptions: {
      // Important part Here
      provider: new OpenStreetMapProvider(),
    },

    marker: {
      id: 1,
      position: { lat: -6.1716001, lng: 106.6405384 },
      tooltip: "Provinsi Banten",
      draggable: false,
      visible: true,
    },

    markers: [],

    geojson: {},
    geojson2: {},
    geojson3: {},
    geojson4: {},
    geojson5: {},

    geostyle: {
      color: "blue",
    },
    geostyle2: {
      color: "blue",
      fillColor: "red",
    },
    geostyle3: {
      color: "blue",
      fillColor: "purple",
    },
    geostyle4: {
      color: "blue",
      fillColor: "yellow",
    },
    geostyle5: {
      color: "blue",
      fillColor: "orange",
    },

    combodataset: [],

    grafik: {
      labels: [],
      datas: [],
      axisx: null,
      axisy: null,
      groupby: null,
      model: "bar",
    },

    componentKey: 0,
  }),
  computed: {
    ...mapState(["page", "device", "theme"]),
  },
  mounted() {
    this.setPage({
      name: "topik",
      crud: false,
    });
    this.fetchDataset().then(() => {
      this.fetchDatasetData();
    });
    this.fetchGeoJson();
    this.fetchGeoJson2();
    this.fetchGeoJson3();
    this.fetchGeoJson4();
    this.fetchGeoJson5();
  },
  computed: {
    ...mapState(["device", "theme", "info", "snackbar", "loading", "http"]),
    options() {
      return {
        onEachFeature: this.onEachFeatureFunction,
      };
    },
    onEachFeatureFunction() {
      return (feature, layer) => {
        layer.bindTooltip(
          "<div>" +
            feature.properties.name +
            "</div><div>JML BTS : " +
            "</div>",
          { permanent: false, sticky: true }
        );
      };
    },
  },
  methods: {
    ...mapActions(["setPage", "getAppInfo", "snackbarClose", "setLoading"]),
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

        data.headers.forEach((element) => {
          const row = {};
          row["value"] = element.value;
          row["text"] = element.text;
          this.combodataset.push(row);
        });
      } catch (error) {}
    },
    fetchDatasetData: async function () {
      try {
        this.loading = true;
        this.records = [];
        let {
          data: { success, code, message, data },
        } = await this.http.get(
          "show-dataset-table/" + this.$route.params.dataset_uuid
        );
        this.records = data;
      } catch (error) {
      } finally {
        this.loading = false;
      }
    },
    fetchGeoJson: async function () {
      let { data } = await this.http.get(
        "https://data.bantenprov.go.id/3602.json"
      );
      this.geojson = data;
    },
    fetchGeoJson2: async function () {
      let { data } = await this.http.get(
        "https://data.bantenprov.go.id/3601.json"
      );
      this.geojson2 = data;
    },
    fetchGeoJson3: async function () {
      let { data } = await this.http.get(
        "https://data.bantenprov.go.id/3603.json"
      );
      this.geojson3 = data;
    },
    fetchGeoJson4: async function () {
      let { data } = await this.http.get(
        "https://data.bantenprov.go.id/3604.json"
      );
      this.geojson4 = data;
    },
    fetchGeoJson5: async function () {
      let { data } = await this.http.get(
        "https://data.bantenprov.go.id/3671.json"
      );
      this.geojson5 = data;
    },

    applyGrafik: function () {
      this.grafik.labels = [];
      this.grafik.datas = [];
      this.records.forEach((element) => {
        const entities = Object.entries(element);
        entities.forEach((item) => {
          const entitykey = item[0];
          const entityval = item[1];
          //set label

          if (this.grafik.axisx == entitykey) {
            this.grafik.labels.push(entityval);
          }
          if (this.grafik.axisy == entitykey) {
            this.grafik.datas.push(entityval);
          }
        });

        this.componentKey += 1;
      });
    },

    postDownload: function (val) {
      window.open(val);
    },
  },
};
</script>

<style>
.embed-container {
  position: relative;
  padding-bottom: 80%;
  height: 0;
  max-width: 100%;
}
.embed-container iframe,
.embed-container object,
.embed-container iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
}
small {
  position: absolute;
  z-index: 40;
  bottom: 0;
  margin-bottom: -15px;
}
</style>