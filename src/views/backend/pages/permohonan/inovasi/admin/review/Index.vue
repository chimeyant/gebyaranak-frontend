<template>
  <div :class="device.desktop ? `home pa-6 grey lighten-4`:`home pa-0 grey lighten-4`">

    <v-row>
      <v-col cols="12">
        <v-card class="animated animate__fadeInUp rounded-0">
          <v-card-title :class="`flex flex-row-reverse ` + theme.color + ` lighten-1`">
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
                  v-show="page.actions.add"
                  class="animate__animated animate__shakeY animate__delay-1s"
                >
                  <v-icon
                    :color="theme.mode == 'dark' ? `white` : `black`"
                    @click="openPermohonanCreate"
                  >add_circle</v-icon>
                </v-btn>
              </template>
              <span>Tambah Data</span>
            </v-tooltip>
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
                >
                  <v-icon
                    :color="theme.mode == 'dark' ? `white` : `black`"
                    @click="$router.push({name:'permohonan-inovasi-publisher'})"
                  >mdi-close-circle</v-icon>
                </v-btn>
              </template>
              <span>Refresh Data</span>
            </v-tooltip>
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
                >
                  <v-icon
                    :color="theme.mode == 'dark' ? `white` : `black`"
                    @click="fetchRecords"
                  >refresh</v-icon>
                </v-btn>
              </template>
              <span>Refresh Data</span>
            </v-tooltip>

            <v-spacer></v-spacer>
            <div class="font-weight-regular subtitle-1 white--text">Lembar Review Inovasi</div>
            <v-icon
              small
              class="orange--text animate__animated animate__flash animate__infinite mr-2"
            >mdi-circle</v-icon>
          </v-card-title>
          <v-card-text>
            <v-col colc="12">
              <v-row class="justify-center mt-2 mb-5">
                <div class="title ">Data Permohonan Inovasi</div>
              </v-row>
              <v-row class="mb-10">
                <v-col cols="8">
                  <tbody>
                    <tr>
                      <td style="width: 150px ;">Nomor Registrasi</td>
                      <td class="pl-2 pr-2">:</td>
                      <td class="font-weight-bold grey--text">{{ record.nomor_register }}</td>
                    </tr>
                    <tr>
                      <td>Judul Inovasi</td>
                      <td class="pl-2 pr-2">:</td>
                      <td class="font-weight-bold">{{ record.name }}</td>
                    </tr>
                    <tr>
                      <td>Jenis Inovasi</td>
                      <td class="pl-2 pr-2">:</td>
                      <td>{{ record.jenisinovasi }}</td>
                    </tr>
                    <tr>
                      <td>Jenis Urusan</td>
                      <td class="pl-2 pr-2">:</td>
                      <td>{{ record.urusan }}</td>
                    </tr>
                    <tr>
                      <td>Inisiator</td>
                      <td class="pl-2 pr-2">:</td>
                      <td>{{ record.inisiator }}</td>
                    </tr>
                    <tr>
                      <td>Bentuk Inovasi</td>
                      <td class="pl-2 pr-2">:</td>
                      <td>{{ record.bentuk }}</td>
                    </tr>
                    <tr>
                      <td>Waktu Uji</td>
                      <td class="pl-2 pr-2">:</td>
                      <td>{{ record.waktu_uji }}</td>
                    </tr>
                    <tr>
                      <td>Waktu Penerapan</td>
                      <td class="pl-2 pr-2">:</td>
                      <td>{{ record.waktu_penerapan }}</td>
                    </tr>
                    <tr>
                      <td>Tahapan</td>
                      <td class="pl-2 pr-2">:</td>
                      <td>{{ record.tahapan }}</td>
                    </tr>
                    <tr>
                      <td>Rancang Bangun</td>
                      <td class="pl-2 pr-2">:</td>
                      <td>{{ record.rancang_bangun }}</td>
                    </tr>
                    <tr>
                      <td>Tujuan Inovasi Daerah</td>
                      <td class="pl-2 pr-2">:</td>
                      <td>{{ record.tujuan }}</td>
                    </tr>
                    <tr>
                      <td>Manfaat Yang Di Peroleh</td>
                      <td class="pl-2 pr-2">:</td>
                      <td>{{ record.manfaat }}</td>
                    </tr>
                    <tr>
                      <td>Hasil</td>
                      <td class="pl-2 pr-2">:</td>
                      <td>{{ record.hasil }}</td>
                    </tr>
                  </tbody>
                  <div class="subtitle-1 mt-5 mb-2 font-weight-bold">Inovator Dan Lokasi</div>
                  <tbody>
                    <tr>
                      <td class="">Nama Inovator</td>
                      <td class="pl-2 pr-2">:</td>
                      <td class="font-weight-bold">{{ record.nama_inovator }}</td>
                    </tr>
                    <tr>
                      <td>Telpon</td>
                      <td class="pl-2 pr-2">:</td>
                      <td>{{ record.telp }}</td>
                    </tr>
                    <tr>
                      <td>Nama Instansi</td>
                      <td class="pl-2 pr-2">:</td>
                      <td>{{ record.instansi }}</td>
                    </tr>
                    <tr>
                      <td>Kabupaten</td>
                      <td class="pl-2 pr-2">:</td>
                      <td>{{ record.kabupaten }}</td>
                    </tr>
                    <tr>
                      <td>Kota</td>
                      <td class="pl-2 pr-2">:</td>
                      <td>{{ record.kecamatan }}</td>
                    </tr>
                    <tr>
                      <td>Kel/Desa</td>
                      <td class="pl-2 pr-2">:</td>
                      <td>{{ record.desa }}</td>
                    </tr>
                    <tr>
                      <td>Alamat</td>
                      <td class="pl-2 pr-2">:</td>
                      <td>{{ record.alamat }}</td>
                    </tr>
                  </tbody>

                </v-col>
                <v-col>
                  <v-card class="shadow-1 rounded-0 white--text">
                    <v-card-title class="subtitle-1 font-weight-regular green">
                      Data Pendukung Lainnya
                    </v-card-title>
                    <v-card-text>
                      <v-col cols="12">
                        <v-row class="mt-4">
                          <v-col cols="4">
                            <div class="btn-container">
                              <div class="btn-icon">
                                <v-icon
                                  large
                                  color="blue"
                                  @click="openPdfView(record.path_file_anggaran)"
                                >mdi-cash-usd</v-icon>
                              </div>
                              <div class="
                                    btn-title">Anggaran
                              </div>
                            </div>
                          </v-col>

                          <v-col cols="4">
                            <div class="btn-container">
                              <div class="btn-icon">
                                <v-icon
                                  large
                                  color="green"
                                  @click="openPdfView(record.path_file_profil_bisnis)"
                                >mdi-google-my-business</v-icon>
                              </div>
                              <div class="btn-title">Profil Bisnis</div>
                            </div>
                          </v-col>

                          <v-col cols="4">
                            <div class="btn-container">
                              <div class="btn-icon">
                                <v-icon
                                  large
                                  color="purple"
                                  @click="openPdfView(record.path_foto_inovasi)"
                                >mdi-camera</v-icon>
                              </div>
                              <div class="btn-title">Foto Inovasi</div>
                            </div>
                          </v-col>

                          <v-col cols="4">
                            <div class="btn-container">
                              <div class="btn-icon">
                                <v-icon
                                  large
                                  color="orange"
                                >mdi-video-high-definition</v-icon>
                              </div>
                              <div class="btn-title">Video</div>
                            </div>
                          </v-col>

                          <v-col cols="4">
                            <div class="btn-container">
                              <div class="btn-icon">
                                <v-icon
                                  large
                                  color="red"
                                >mdi-youtube</v-icon>
                              </div>
                              <div class="btn-title">YouTube</div>
                            </div>
                          </v-col>

                          <v-col cols="4">
                            <div class="btn-container">
                              <div class="btn-icon">
                                <v-icon
                                  large
                                  color="brown"
                                >mdi-map</v-icon>
                              </div>
                              <div class="btn-title">Peta</div>
                            </div>
                          </v-col>

                        </v-row>
                      </v-col>
                    </v-card-text>
                  </v-card>
                </v-col>
              </v-row>
              <v-row>
                <v-col cols=12>
                  <v-divider></v-divider>
                </v-col>
                <v-col cols="12">
                  <v-tabs
                    v-model="tab"
                    centered
                    :color="theme.color"
                  >
                    <v-tabs-slider></v-tabs-slider>

                    <v-tab
                      href="#tab-1"
                      class=""
                    >
                      <v-icon
                        class="mr-2"
                        color="red"
                      >mdi-bank</v-icon>
                      Profil PEMDA
                    </v-tab>

                    <v-tab href="#tab-2">
                      <v-icon
                        class="mr-2"
                        color="orange"
                      >mdi-brightness-percent</v-icon>
                      Indikator Pemda

                    </v-tab>

                    <v-tab href="#tab-3">
                      <v-icon
                        class="mr-2"
                        color="blue"
                      >mdi-brightness-7</v-icon>
                      Indikator Inovasi

                    </v-tab>
                  </v-tabs>

                  <v-tabs-items v-model="tab">
                    <v-tab-item
                      key="0"
                      value="tab-1"
                    >
                      <v-card flat>
                        <v-card-text>
                          <v-row class="ml-2 mr-2 mt-5">
                            <tbody>
                              <tr>
                                <td style="width:100px">Nama</td>
                                <td class="pl-2 pr-2">:</td>
                                <td class="font-weight-bold">{{ profilepemda.record.name }}</td>
                              </tr>
                              <tr>
                                <td style="width:100px">Nama Admin</td>
                                <td class="pl-2 pr-2">:</td>
                                <td>{{ profilepemda.record.nama_admin }}</td>
                              </tr>
                              <tr>
                                <td style="width:100px">Jabatan Admin</td>
                                <td class="pl-2 pr-2">:</td>
                                <td>{{ profilepemda.record.jabatan_admin }}</td>
                              </tr>
                              <tr>
                                <td style="width:100px">Email</td>
                                <td class="pl-2 pr-2">:</td>
                                <td>{{ profilepemda.record.email }}</td>
                              </tr>
                              <tr>
                                <td style="width:100px">Telp</td>
                                <td class="pl-2 pr-2">:</td>
                                <td>{{ profilepemda.record.phone }}</td>
                              </tr>
                              <tr>
                                <td style="width:100px">Fakta Integritas</td>
                                <td class="pl-2 pr-2">:</td>
                                <td><v-btn
                                    small
                                    outlined
                                    dense
                                    hide-detail
                                    :color="theme.color"
                                    @click="openPdfView(profilepemda.record.path_file_fakta_integritas)"
                                  > <v-icon
                                      small
                                      class="mr-2"
                                    >mdi-eye</v-icon>Lihat Dokumen</v-btn></td>
                              </tr>
                            </tbody>

                          </v-row>
                        </v-card-text>
                      </v-card>
                    </v-tab-item>

                    <v-tab-item
                      key="1"
                      value="tab-2"
                    >
                      <v-card flat>
                        <v-row class="ml-1 mr-1 mt-5">
                          <v-col cols="8">
                            <v-card flat>
                              <v-data-table
                                :headers="indikatorpemda.headers"
                                :items="indikatorpemda.records"
                                :items-per-page="10"
                                class="elevation-2 mb-1"
                                :color="theme.color"
                                :loading="loading.table"
                                loading-text="Loading... Please wait"
                                :search="search"
                              >
                                <template v-slot:item.datadisplay.id="{ value }">
                                  <v-icon
                                    @click="postProfileDocument(value)"
                                    color="orange"
                                  >mdi-folder</v-icon>
                                </template>
                              </v-data-table>
                            </v-card>
                          </v-col>
                          <v-col cols="4">
                            <v-card class="shadow-1 rounded-0 white--text">
                              <v-card-title class="subtitle-1 font-weight-regular green">
                                Daftar Dokumen Pendukung
                              </v-card-title>
                              <v-card-text>
                                <v-row class="mt-3 pl-2 pr-2">
                                  <v-col
                                    cols="4"
                                    v-for="(item,index) in indikatorpemda.documents"
                                  >
                                    <div class="file-container">
                                      <div>
                                        <v-icon
                                          @click="openPdfView(item.path_document)"
                                          color="red"
                                        >mdi-file-pdf</v-icon>
                                      </div>
                                      <div class="file-title">
                                        {{ item.nomor_dokumen }}
                                      </div>
                                    </div>
                                  </v-col>

                                </v-row>
                              </v-card-text>
                            </v-card>
                          </v-col>
                        </v-row>
                      </v-card>
                    </v-tab-item>

                    <v-tab-item
                      key="2"
                      value="tab-3"
                    >
                      <v-row class="ml-1 mr-1 mt-5">
                        <v-col cols="8">
                          <v-card flat>
                            <v-data-table
                              :headers="indikatorinovasi.headers"
                              :items="indikatorinovasi.records"
                              :items-per-page="10"
                              class="elevation-2 mb-1"
                              :color="theme.color"
                              :loading="loading.table"
                              loading-text="Loading... Please wait"
                              :search="search"
                            >
                              <template v-slot:item.datadisplay.id="{ value }">
                                <v-icon
                                  @click="postInovasiDocument(value)"
                                  color="orange"
                                >mdi-folder</v-icon>
                              </template>
                            </v-data-table>
                          </v-card>
                        </v-col>
                        <v-col cols="4">
                          <v-card class="shadow-1 rounded-0 white--text">
                            <v-card-title class="subtitle-1 font-weight-regular green">
                              Daftar Dokumen Pendukung
                            </v-card-title>
                            <v-card-text>
                              <v-row class="mt-3 pl-2 pr-2">
                                <v-col
                                  cols="4"
                                  v-for="(item,index) in indikatorinovasi.documents"
                                >
                                  <div class="file-container">
                                    <div>
                                      <v-icon
                                        @click="openPdfView(item.path_document)"
                                        color="red"
                                      >mdi-file-pdf</v-icon>
                                    </div>
                                    <div class="file-title">
                                      {{ item.nomor_dokumen }}
                                    </div>
                                  </div>
                                </v-col>

                              </v-row>
                            </v-card-text>
                          </v-card>
                        </v-col>
                      </v-row>
                    </v-tab-item>

                  </v-tabs-items>
                </v-col>
              </v-row>
            </v-col>

          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <v-col cols="12">
      <v-dialog
        transition="dialog-bottom-transition"
        v-model="form.add"
        :max-width="device.desktop ? `600px` : `100%`"
        persistent
        :fullscreen="device.mobile"
      >
        <v-card>
          <v-toolbar
            :color="theme.color"
            :dark="theme.mode"
          >
            <v-icon
              small
              color="orange"
              class="mr-1 animate__animated animate__flash animate__infinite"
            >mdi-circle</v-icon> Formulir Master Indikator
          </v-toolbar>
          <v-card-text class="mt-2">
            <v-col cols="12">
              <v-select
                label="Kategori"
                outlined
                dense
                hide-details
                v-model="record.category_uuid"
                :items="categories"
              ></v-select>
            </v-col>
            <v-col col="12">
              <v-text-field
                outlined
                :color="theme.color"
                hide-details
                label="*Indikator"
                placeholder=""
                v-model="record.name"
                :filled="record.name"
                dense
              ></v-text-field>
            </v-col>
            <v-col col="12">
              <v-text-field
                outlined
                :color="theme.color"
                hide-details
                label="*Skor"
                placeholder=""
                v-model="record.skor"
                :filled="record.skor"
                dense
              ></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-switch
                label="Status"
                outlined
                dense
                hide-detail
                v-model="record.status"
                :color="theme.color"
              ></v-switch>
            </v-col>
          </v-card-text>

          <v-divider></v-divider>
          <v-card-actions class="justify-end">
            <v-btn
              outlined
              :color="theme.color"
              v-show="!form.edit"
              @click="postAddNewRecord"
            >Tambah</v-btn>
            <v-btn
              outlined
              :color="theme.color"
              v-show="form.edit"
              @click="postUpdateRecord"
            >Ubah</v-btn>
            <v-btn
              outlined
              color="grey"
              @click="closeForm"
            >Batal</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-col>
    <v-col cols="12">
      <v-dialog
        transition="dialog-bottom-transition"
        v-model="verifikasi.show"
        :max-width="device.desktop ? `600px` : `100%`"
        persistent
        :fullscreen="device.mobile"
      >
        <v-card>
          <v-toolbar
            :color="theme.color"
            :dark="theme.mode"
          >
            <v-icon
              small
              color="orange"
              class="mr-1 animate__animated animate__flash animate__infinite"
            >mdi-circle</v-icon> Formulir Verifikasi Status
          </v-toolbar>
          <v-card-text class="mt-2">
            <v-col col="12">
              <v-textarea
                outlined
                :color="theme.color"
                hide-details
                label="Pesan"
                placeholder=""
                v-model="verifikasi.record.content"
                :filled="verifikasi.record.content"
                rows="3"
                dense
              ></v-textarea>
            </v-col>
            <v-col cols="12">
              <v-select
                label="Status"
                outlined
                dense
                hide-details
                v-model="verifikasi.record.status"
                :items="verifikasi.status"
                :color="theme.color"
              ></v-select>
            </v-col>

          </v-card-text>

          <v-divider></v-divider>
          <v-card-actions class="justify-end">
            <v-btn
              outlined
              :color="theme.color"
              @click="postVerfikasiStatus"
            >Kirim</v-btn>

            <v-btn
              outlined
              color="grey"
              @click="closeFormStatusVerfikasi"
            >Batal</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-col>

    <v-col cols="12">
      <v-dialog
        transition="dialog-bottom-transition"
        v-model="pdfview.show"
        :max-width="device.desktop ? `60%` : `100%`"
        persistent
        :fullscreen="device.mobile"
      >
        <v-card>
          <v-toolbar
            :color="theme.color"
            :dark="theme.mode"
          >
            <v-icon
              small
              color="orange"
              class="mr-1 animate__animated animate__flash animate__infinite"
            >mdi-circle</v-icon> Lihat Dokumen
          </v-toolbar>

          <v-row>
            <v-col cols="12">
              <iframe
                :src="pdfview.url"
                frameborder="0"
                class="pdfview"
              ></iframe>
            </v-col>
          </v-row>
          <v-card-actions class="justify-end">
            <v-btn
              outlined
              color="grey"
              @click="closePdfView"
            >Tutup</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-col>
  </div>
</template>
              <script>
import { mapActions, mapState } from "vuex";
import "animate.css";

export default {
  name: "permohonan-inovasi",
  data: () => ({
    num: 1,
    tab: null,

    profilepemda: {
      record: {},
    },

    indikatorpemda: {
      headers: [
        {
          text: "Nama Indikator",
          align: "start",
          sortable: true,
          value: "indikatorpemda.datadisplay.name",
        },
        {
          text: "Informasi",
          align: "start",
          sortable: true,
          value: "informasi",
        },
        {
          text: "Jml.Dok",
          align: "center",
          sortable: false,
          value: "datadisplay.jmldoc",
          width: 100,
        },
        {
          text: "Aksi",
          align: "center",
          sortable: false,
          value: "datadisplay.id",
          width: 100,
        },
      ],
      records: [],
      documents: [],
    },
    indikatorinovasi: {
      headers: [
        {
          text: "Nama Indikator",
          align: "start",
          sortable: true,
          value: "datadisplay.name",
        },
        {
          text: "Informasi",
          align: "start",
          sortable: true,
          value: "datadisplay.informasi.text",
        },
        {
          text: "Jml.Dok",
          align: "center",
          sortable: false,
          value: "datadisplay.jmldoc",
          width: 100,
        },
        {
          text: "Aksi",
          align: "center",
          sortable: false,
          value: "datadisplay.id",
          width: 100,
        },
      ],
      records: [],
      documents: [],
    },
    status: [
      { text: "Dokumen Terverifikasi", value: "4" },
      {
        text: "Subtansi Terverifikasi",
        value: "5",
      },
      {
        text: "Ditolak, Perlu Perbaikan",
        value: "2",
      },
    ],

    search: null,
    filename: null,
    categories: [],
    verifikasi: {
      show: false,
      record: {},
      status: [
        { text: "Dokumen Terverifikasi", value: "4" },
        {
          text: "Subtansi Terverifikasi",
          value: "5",
        },
        {
          text: "Ditolak, Perlu Perbaikan",
          value: "2",
        },
      ],
    },
    pdfview: {
      show: false,
      url: "/",
    },
  }),
  computed: {
    ...mapState([
      "page",
      "theme",
      "http",
      "device",
      "record",
      "records",
      "loading",
      "event",
      "snackbar",
      "table",
      "form",
    ]),
    filterItems() {
      if (this.search != null) {
        return this.records.filter((item) => {
          return (
            item.name.toLowerCase().indexOf(this.search.toLowerCase()) > -1
          );
        });
      } else {
        return this.records;
      }
    },
  },
  created() {
    this.setPage({
      crud: true,
      dataUrl: "",
      pagination: false,
      key: "id",
      title: "REVIEW PERMOHONAN",
      subtitle: "Lembar Formulir Review Permohonan",
      breadcrumbs: [
        {
          text: "Permohonan",
          disabled: true,
          href: "",
        },
        {
          text: "Review",
          disabled: true,
          href: "",
        },
      ],
      showtable: false,
      actions: {
        refresh: true,
        add: false,
        edit: false,
        delete: false,
        bulkdelete: false,
        print: false,
        export: false,
        help: false,
      },
    });
  },
  mounted() {
    this.fetchRecords();
  },
  methods: {
    ...mapActions([
      "setPage",
      "postAddNew",
      "postEdit",
      "postUpdate",
      "postConfirmDelete",
      "assignFileBrowse",
      "setLoading",
      "setRecord",
      "setForm",
    ]),
    fetchRecords: async function () {
      try {
        let { data } = await this.http.get(
          "api/v2/permohonan/verifikator/inovasi/" + this.$route.params.id
        );
        this.setRecord(data);
        this.indikatorinovasi.records = data.inovasiindikators;
        this.fetchProfile();
      } catch (error) {}
    },
    fetchProfile: async function () {
      try {
        let { data } = await this.http.get(
          "api/v2/permohonan/verifikator/profile-show/" +
            this.record.regency_code
        );
        this.profilepemda.record = data;
        this.indikatorpemda.records = data.indikator;
      } catch (error) {}
    },

    openForm: function () {
      this.setForm({
        add: true,
        edit: false,
      });
      this.setRecord({});
    },
    closeForm: function () {
      this.setForm({
        add: false,
        edit: false,
      });
    },
    postAddNewRecord: function () {
      this.postAddNew(this.record).then(() => {
        this.closeForm();
      });
    },
    editRecord: function (val) {
      this.postEdit(val).then(() => {
        this.filename = this.record.icon;
      });
      this.setForm({
        add: true,
        edit: true,
      });
    },
    postUpdateRecord: function () {
      this.postUpdate(this.record).then(() => {
        this.closeForm();
      });
    },
    postDeleteRecord: function (val) {
      this.postConfirmDelete(val);
    },
    postDownload(val) {
      window.open(val, "__blank");
    },
    uploadFile: function () {
      this.assignFileBrowse({
        fileType: [".png", ".jpg", ".jpeg"],
        query: {
          doctype: "apps",
        },
        callback: (response) => {
          setTimeout(() => {
            this.filename = response.name;
            this.record.icon = response.name;
          }, 500);
        },
      });
    },
    fetchCategories: async function () {
      try {
        let { data } = await this.http.get("api/v2/combo/category");
        this.categories = data;
      } catch (error) {}
    },
    openPermohonanCreate: function () {
      this.$router.push({
        name: "permohonan-inovasi-opd-create",
      });
    },
    openIndikator: function (val) {
      this.$router.push({
        name: "permohonan-inovasi-opd-indikator",
        params: {
          inovasi_uuid: val,
        },
      });
    },
    postPush: async function (val) {
      try {
        this.setLoading({ dialog: true, text: "Proses pengiriman permohonan" });
        let {
          data: { code, success, message, error },
        } = await this.http.post("api/v2/permohonan/opd/inovasi-push", {
          id: val,
        });

        if (!success) {
          this.snackbar.color = "orange";
          this.snackbar.text = message;
          this.snackbar.state = true;
          return;
        }

        this.snackbar.color = this.theme.color;
        this.snackbar.text = message;
        this.snackbar.state = true;

        this.fetchRecords();
      } catch (error) {
        this.snackbar.color = "red";
        this.snackbar.text = "Opps..., terjadi kesalahan";
        this.snackbar.state = true;
      } finally {
        this.setLoading({ dialog: false, text: "" });
      }
    },
    postPull: async function (val) {
      try {
        this.setLoading({ dialog: true, text: "Proses pembatalan permohonan" });
        let {
          data: { code, success, message, error },
        } = await this.http.post("api/v2/permohonan/opd/inovasi-pull", {
          id: val,
        });

        if (!success) {
          this.snackbar.color = "orange";
          this.snackbar.text = message;
          this.snackbar.state = true;
          return;
        }

        this.snackbar.color = this.theme.color;
        this.snackbar.text = message;
        this.snackbar.state = true;

        this.fetchRecords();
      } catch (error) {
        this.snackbar.color = "red";
        this.snackbar.text = "Opps..., terjadi kesalahan";
        this.snackbar.state = true;
      } finally {
        this.setLoading({ dialog: false, text: "" });
      }
    },
    openFormStatusVerfikasi: function (val) {
      this.verifikasi.record = {};
      this.verifikasi.show = true;
      this.verifikasi.record.inovasi_uuid = val;
    },
    closeFormStatusVerfikasi: function () {
      this.verifikasi.show = false;
      this.verifikasi.record = {};
    },
    postVerfikasiStatus: async function () {
      try {
        this.setLoading({ dialog: true, text: "Proses verifikasi..." });
        let {
          data: { code, success, message, error },
        } = await this.http.post(
          "api/v2/permohonan/verifikator/inovasi-set-status",
          this.verifikasi.record
        );
        if (!success) {
          this.snackbar.color = "orange";
          this.snackbar.text = message;
          this.snackbar.state = true;
          return;
        }
        this.snackbar.color = this.theme.color;
        this.snackbar.text = message;
        this.snackbar.state = true;
        this.fetchRecords();
        this.closeFormStatusVerfikasi();
      } catch (error) {
        this.snackbar.color = "red";
        this.snackbar.text = "Opps.., terjadi kesalahan ";
        this.snackbar.state = false;
      } finally {
        this.setLoading({ dialog: false, text: "" });
      }
    },
    postProfileDocument: async function (val) {
      try {
        let { data } = await this.http.get(
          "api/v2/permohonan/verifikator/profile-document/" + val
        );

        this.indikatorpemda.documents = data;
      } catch (error) {}
    },
    postInovasiDocument: async function (val) {
      try {
        let { data } = await this.http.get(
          "api/v2/permohonan/verifikator/inovasi-document/" + val
        );
        this.indikatorinovasi.documents = data;
      } catch (error) {}
    },

    /**
     * Componsen
     */
    openPdfView: function (url) {
      this.pdfview.url = url;
      this.pdfview.show = true;
    },
    closePdfView: function () {
      this.pdfview.url = "/";
      this.pdfview.show = false;
    },

    /**
     * Hasil Verifikasi
     */
    postHasil: async function () {
      try {
        this.setLoading({ dialog: true, text: "Proses verifikasi..." });
        let {
          data: { code, success, message, error },
        } = await this.http.post(
          "api/v2/permohonan/verifikator/inovasi-set-status",
          {
            content: this.record.content,
            status: this.record.status,
            inovasi_uuid: this.record.id,
          }
        );
        if (!success) {
          this.snackbar.color = "orange";
          this.snackbar.text = message;
          this.snackbar.state = true;
          return;
        }
        this.snackbar.color = this.theme.color;
        this.snackbar.text = message;
        this.snackbar.state = true;
        this.$router.push({
          name: "permohonan-inovasi-verifikator",
        });
      } catch (error) {
        this.snackbar.color = "red";
        this.snackbar.text = "Opps.., terjadi kesalahan ";
        this.snackbar.state = false;
      } finally {
        this.setLoading({ dialog: false, text: "" });
      }
    },
  },
};
</script>
  
  <style>
.btn-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.btn-icon {
  height: 50px;
  width: 50px;
  display: flex;
  border: 2px solid green;
  border-radius: 5px;
  justify-content: center;
  overflow: hidden;
}
.btn-title {
  width: 100px;
  display: flex;
  justify-content: center;
  font-size: 9pt;
}
.file-container {
  display: flex;
  justify-items: center;
  flex-direction: column;
  align-items: center;
}
.file-title {
  text-align: center;
  font-size: 10pt;
}
.pdfview {
  width: 100%;
  height: 70vh;
}
</style>