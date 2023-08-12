<template>
  <div class="mt-10">
    <v-container>
      <v-row>
        <h3 class="display-1 font-weight-bold">Dataset</h3>
        <v-spacer></v-spacer>
        <v-btn
          outlined
          class="indigo--text"
        >Lacak Permohonan Dataset</v-btn>
        <v-btn
          class="indigo ml-2 white--text elevation-0"
          @click="openPermohonan"
        >Permohonan Dataset</v-btn>
      </v-row>
      <v-row class="mt-10 text-body-2">
        Temukan kumpulan data-data mentah berupa tabel yang bisa diolah lebih lanjut di sini. Open Data Banten menyediakan akses ke beragam koleksi dataset dari seluruh Organisasi Perangkat Daerah di Provinsi Banten.
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
                  src="/images/search-topik.jpeg"
                  alt=""
                  srcset=""
                  width="300"
                  class="animate__animated animate__fadeInRight"
                >
              </v-col>
              <v-col cols="8">
                <span class="mt-5 text-h6 animate__animated animate__fadeInUp animate__delay-1s">
                  Apa saja yang bisa dilakukan dengan Dataset? Temukan banyak hal tentang Banten melalui berbagai koleksi data sesuai kebutuhan di sini.
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
              placeholder="Pencarian dataset"
              append-icon="search"
              color="orange"
            ></v-text-field>
          </v-col>
          <v-col cols="12">
            <v-row class="pl-3 pr-3 pt-5">
              <span class="text-body-2 font-weight-medium">
                {{ datas.meta.total }} Dataset ditemukan
              </span>
              <v-spacer>
              </v-spacer>
              <v-select
                label="Urutkan"
                outlined
                dense
                style="max-width: 300px;"
                :items="ururtans"
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
                      class="mr-2 mb-2 rounded-lg"
                    >
                    <v-list-item-content class="mr-5">
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
                            @click="openDatasetDetail(item.id)"
                          >Lihat Dataset</v-btn>
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
                      <div></div>
                    </v-list-item-content>
                    <v-list-item-action>
                      <div>
                        <v-icon
                          small
                          class="mr-2"
                        >mdi-eye</v-icon><span class="text-body-2">{{ item.counter }}</span>
                      </div>
                    </v-list-item-action>
                  </v-list-item>
                </template>
              </v-list>

              <v-row class="justify-end mt-10 ">
                <div class="mt-4 mb-5">
                  <v-select
                    label="Per Halaman"
                    outlined
                    dense
                    :items="perHalaman"
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
        <v-col cols="12">
          <v-dialog
            transition="dialog-bottom-transition"
            v-model="permohonan.show"
            :max-width="device.desktop ? `600px` : `100%`"
            persistent
            :fullscreen="device.mobile"
          >
            <v-card>
              <v-toolbar
                :color="theme.color"
                :dark="theme.mode"
              >
                <v-icon class="mr-1">mdi-circle</v-icon> Formulir Permohonan Dataset
              </v-toolbar>
              <v-card-text class="mt-2">

                <v-col cols="12">
                  <v-row>
                    <v-col cols="12">
                      <span class="grey--text font-weight-bolder">IDENTITAS</span>
                    </v-col>
                    <v-col cols="12">
                      <v-text-field
                        label="Nama"
                        :color="theme.color"
                        outlined
                        dense
                        hide-details
                        v-model="permohonan.record.name"
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12">
                      <v-text-field
                        label="Email"
                        :color="theme.color"
                        outlined
                        dense
                        hide-details
                        v-model="permohonan.record.email"
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12">
                      <v-text-field
                        label="Nomor Telpon"
                        :color="theme.color"
                        outlined
                        dense
                        hide-details
                        v-model="permohonan.record.telp"
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12">
                      <v-divider></v-divider>
                    </v-col>
                    <v-col cols="12">
                      <span class="grey--text font-weight-bolder">INFORMASI PEKERJAAN</span>
                    </v-col>
                    <v-col cols=12>
                      <v-select
                        label="Pekerjaan"
                        outlined
                        dense
                        hide-details
                        :color="theme.color"
                        v-model="permohonan.record.pekerjaan"
                        :items="permohonan.perkerjaans"
                      ></v-select>
                    </v-col>
                    <v-col cols="12">
                      <span class="grey--text font-weight-bolder">KEBUTUHAN DATASET</span>
                    </v-col>
                    <v-col cols="12">
                      <v-textarea
                        label="Judul Kebutuhan Dataset"
                        :color="theme.color"
                        outlined
                        dense
                        hide-details
                        v-model="permohonan.record.kebutuhan"
                        rows="3"
                      >{{ permohonan.record.kebutuhan }}</v-textarea>
                    </v-col>
                    <v-col cols="12">
                      <v-textarea
                        label="Penjelasan Kebutuhan Dataset"
                        :color="theme.color"
                        outlined
                        dense
                        hide-details
                        v-model="permohonan.record.keterangan"
                        rows="3"
                      >{{ permohonan.record.kebutuhan }}</v-textarea>
                    </v-col>
                    <v-col cols=12>
                      <v-select
                        label="Tujuan Kebutuhan Dataset"
                        outlined
                        dense
                        hide-details
                        :color="theme.color"
                        v-model="permohonan.record.tujuan"
                        :items="permohonan.tujuans"
                      ></v-select>
                    </v-col>
                  </v-row>
                </v-col>
              </v-card-text>
              <v-divider></v-divider>
              <v-card-actions class="justify-end">
                <v-btn
                  outlined
                  :color="theme.color"
                  @click="postPermohonan"
                >Kirim</v-btn>

                <v-btn
                  outlined
                  color="grey"
                  @click="closePermohonan"
                >Batal</v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";
export default {
  name: "modul-dataset",
  data: () => ({
    page: 1,
    perHalaman: [
      { text: 5, value: 5 },
      { text: 10, value: 10 },
      { text: 25, value: 25 },
      { text: 50, value: 50 },
    ],
    ururtans: [
      { text: "Terbaru", value: "terbaru" },
      { text: "Terlama", value: "terlama" },
      { text: "A-Z", value: "az" },
      { text: "Z-A", value: "za" },
    ],

    datas: [],

    permohonan: {
      show: false,
      record: {},
      perkerjaans: [
        { text: "Pelajar", value: "pelajar" },
        { text: "Mahasiswa", value: "mahasiswa" },
        { text: "Akademisi", value: "akademisi" },
        { text: "Profesional", value: "profesional" },
        { text: "Lainnya", value: "lainnya" },
      ],
      tujuans: [
        { text: "Referensi Kajian Bisnis", value: "ref-bisnis" },
        { text: "Referensi Pembuatan Kebijakan", value: "ref-kebijakan" },
        { text: "Referensi Karya Ilmiah", value: "ref-ilmiah" },
        { text: "Referensi Probadi", value: "ref-pribadi" },
        { text: "Lainnya", value: "lainnya" },
      ],
    },
  }),

  mounted() {
    this.setPage({
      name: "topik",
      crud: false,
    });
    this.fetchDatasets();
  },
  computed: {
    ...mapState(["device", "theme", "info", "snackbar", "loading", "http"]),
  },
  methods: {
    ...mapActions(["setPage", "getAppInfo", "snackbarClose", "setLoading"]),
    fetchDatasets: async function () {
      try {
        let { data } = await this.http.get("katalog/dataset");
        this.datas = data;
        this.perPage = "10";
      } catch (error) {}
    },
    openDatasetDetail: async function (val) {
      this.$router.push({
        name: "dataset-detail",
        params: {
          dataset_uuid: val,
        },
      });
    },
    openPermohonan: function () {
      this.permohonan.show = true;
      this.permohonan.record = {};
    },
    closePermohonan: function () {
      this.permohonan.show = false;
    },
    postPermohonan: async function () {
      try {
        this.setLoading({ dialog: true, text: "Proses kirim permohonan" });
        let {
          data: { success, code, message, errors },
        } = await this.http.post("permohonan", this.permohonan.record);

        if (!success) {
          this.snackbar.color = "red";
          this.snackbar.text = message;
          this.snackbar.state = true;
          return;
        }
        this.snackbar.color = this.theme.color;
        this.snackbar.text = message;
        this.snackbar.state = true;
        this.closePermohonan();
      } catch (error) {
        this.snackbar.color = "red";
        this.snackbar.text = "Opps..., terjadi kesalahan";
        this.snackbar.state = true;
      } finally {
        this.setLoading({ dialog: false, text: "" });
      }
    },
  },
};
</script>