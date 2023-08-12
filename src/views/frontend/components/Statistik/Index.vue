<template>
  <div
    class="statistik-container"
    style="background-image: url('images/satudata_bg.png')"
  >
    <v-container>
      <v-col cols="12">
        <div class="statistik-title pb-10 ">
          <h2 class="text-center">Statistik Jenis Data Terbuka Provinsi Banten</h2>
        </div>
        <div>
          <v-row class="justify-center mb-10">
            <v-col :cols="device.desktop ? 3:12">
              <v-card
                class="card-ant"
                height="250"
              >
                <v-card-text>
                  <v-row class="mb-2 ">
                    <v-icon class="white--text mr-2">mdi-circle</v-icon>
                    <div class="font-weight-bold mt-1  teal--text ">
                      Total Data Statistik
                    </div>
                  </v-row>
                  <div class="text-center mt-5">
                    <v-chip
                      color="teal"
                      large
                    >

                      <h2 class="display-1 font-weight-bold white--text text-center">{{ groupdatas.jmlstatistik }} </h2>
                    </v-chip>
                  </div>

                  <div class="mt-5">
                    Kumpulan data-data mentah data-data group statistik
                  </div>
                </v-card-text>
              </v-card>
            </v-col>

            <v-col :cols="device.desktop ? 3:12">
              <v-card
                class="card-ant"
                height="250"
              >
                <v-card-text>
                  <v-row class="mb-2 ">
                    <v-icon class="white--text mr-2">mdi-circle</v-icon>
                    <div class="font-weight-bold mt-1  teal--text ">
                      Total Data Keuangan
                    </div>
                  </v-row>
                  <div class="text-center mt-5">
                    <v-chip
                      color="teal"
                      large
                    >

                      <h2 class="display-1 font-weight-bold white--text text-center">{{ groupdatas.jmlkeuangan }} </h2>
                    </v-chip>
                  </div>

                  <div class="mt-5">
                    Kumpulan data-data mentah berupa data-data group keuangan
                  </div>

                </v-card-text>
              </v-card>
            </v-col>

            <v-col :cols="device.desktop ? 3:12">
              <v-card
                class="card-ant"
                height="250"
              >
                <v-card-text>
                  <v-row class="mb-2 ">
                    <v-icon class="white--text mr-2">mdi-circle</v-icon>
                    <div class="font-weight-bold mt-1  teal--text ">
                      Total Data Geospasial
                    </div>
                  </v-row>
                  <div class="text-center mt-5">
                    <v-chip
                      color="teal"
                      large
                    >

                      <h2 class="display-1 font-weight-bold white--text text-center">{{ groupdatas.jmlgeospasial }} </h2>
                    </v-chip>
                  </div>

                  <div class="mt-5">
                    Kumpulan data-data mentah berupa data-data Geospasial
                  </div>
                </v-card-text>
              </v-card>
            </v-col>

          </v-row>
        </div>
      </v-col>
      <div class="statistik-title pb-10">
        <h2 class="text-center">Statistik Portal Data Terbuka Provinsi Banten</h2>
      </div>
      <div>
        <v-row>
          <v-col :cols="device.desktop ? 3:12">
            <v-card
              class="card-ant"
              height="250"
            >
              <v-card-text>
                <v-row class="mb-2 ">
                  <v-icon class="white--text mr-2">mdi-circle</v-icon>
                  <div class="font-weight-bold mt-1  teal--text ">
                    Total Dataset
                  </div>
                </v-row>
                <div class="text-center mt-5">
                  <v-chip
                    color="teal"
                    large
                  >

                    <h2 class="display-1 font-weight-bold white--text text-center">{{ jmldataset }} </h2>
                  </v-chip>

                </div>

                <div class="mt-5">
                  Kumpulan data-data mentah berupa tabel yang dapat diolah lebih lanjut
                </div>
              </v-card-text>
            </v-card>
          </v-col>
          <v-col :cols="device.desktop ? 3:12">
            <v-card
              height="250"
              class="card-ant"
            >
              <v-card-text>
                <v-row class="mb-2 ">
                  <v-icon class="white--text mr-2">mdi-circle</v-icon>
                  <div class="font-weight-bold mt-1  teal--text ">
                    Total Visualisasi
                  </div>
                </v-row>
                <div class="text-center mt-5">
                  <v-chip
                    color="teal"
                    large
                  >

                    <h2 class="display-1 font-weight-bold white--text text-center">{{ jmldatavisualisasi }} </h2>
                  </v-chip>

                </div>

                <div class="mt-5">
                  Gambaran Informasi data tertentu dalam bentuk grafik
                </div>
              </v-card-text>
            </v-card>
          </v-col>
          <v-col :cols="device.desktop ? 3:12">
            <v-card
              class="card-ant"
              height="250"
            >
              <v-card-text>
                <v-row class="mb-2 ">
                  <v-icon class="white--text mr-2">mdi-circle</v-icon>
                  <div class="font-weight-bold mt-1  teal--text ">
                    Total Infografis
                  </div>
                </v-row>
                <div class="text-center mt-5">
                  <v-chip
                    color="teal"
                    large
                  >

                    <h2 class="display-1 font-weight-bold white--text text-center">{{ jmldatainfografik }} </h2>
                  </v-chip>

                </div>

                <div class="mt-5 ">
                  Informasi yang disajikan dalam bentuk grafik data, sehingga akan lebih mudah untuk dipahami
                </div>
              </v-card-text>
            </v-card>
          </v-col>
          <v-col :cols="device.desktop ? 3:12">
            <v-card
              class="card-ant"
              height="250"
            >
              <v-card-text class="">

                <v-row class="mb-2 ">
                  <v-icon class="white--text mr-2">mdi-circle</v-icon>
                  <div class="font-weight-bold mt-1  teal--text ">
                    Total Videografis
                  </div>
                </v-row>
                <div class="text-center mt-5">
                  <v-chip
                    color="teal"
                    large
                  >

                    <h2 class="display-1 font-weight-bold white--text text-center">{{ jmldatavideografis }} </h2>
                  </v-chip>

                </div>

                <div class="mt-5 ">
                  Videografis yang publikasi datanya tampil di Open Data Provinsi Banten
                </div>

              </v-card-text>
            </v-card>
          </v-col>

        </v-row>

      </div>
    </v-container>
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";
import Bar from "../../../backend/pages/chart/Inflasi.vue";
export default {
  name: "statistic",
  components: {
    Bar,
  },
  data: () => ({
    groupdatas: {
      jmlstatistik: 0,
      jmlkeuangan: 0,
      jmlgeospasial: 0,
    },
    jmldataset: 0,
    jmldatavisualisasi: 0,
    jmldatainfografik: 0,
    jmldatavideografis: 0,
  }),

  computed: {
    ...mapState(["page", "device", "http"]),
  },

  created() {
    this.setPage({
      crud: true,
    });
    this.fetchHomes();
  },
  methods: {
    ...mapActions(["setPage"]),
    fetchHomes: async function () {
      try {
        let {
          data: { data },
        } = await this.http.get("home");
        this.groupdatas.jmlstatistik = data.jmldatastatistik;
        this.groupdatas.jmlkeuangan = data.jmldatakeuangan;
        this.groupdatas.jmlgeospasial = data.jmldatageospasial;
        this.jmldataset = data.jmldataset;
        this.jmldatavisualisasi = data.jmldatavisualisasi;
        this.jmldatainfografik = data.jmldatainfografik;
        this.jmldatavideografis = data.jmldatavideografis;
      } catch (error) {}
    },
  },
};
</script>

<style>
.statistik-container {
  padding-top: 50px;
  padding-bottom: 50px;
  background-color: grey;
  background-size: cover;
}

.statistik-title {
  margin-bottom: 20px;
}
.statistic-card-bg {
  background: darkgrey;
  border-radius: 15px;
}
.card-ant {
  background-image: url("/images/bg-card.jpeg");
  background-size: cover;
}
</style>