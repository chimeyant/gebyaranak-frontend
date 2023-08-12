<template>
  <div :class="device.desktop ? `home pa-6 grey lighten-4`:`home pa-0 grey lighten-4`">
    <v-row
      v-if="!record"
      class="justify-center justify-content-center"
    >
      <v-card max-width="400">
        <v-card-text>
          <p class="justify-center">
            Anda sepertinya belum memiliki profil Pemerintahan Daerah, silahkan membuat profil terlebih dahulu dengan mengklik tombol di bawah ini
          </p>
        </v-card-text>
        <v-card-actions class="justify-center">
          <v-btn
            :color="theme.color"
            outlined
            dense
            class="mb-3"
            @click="postAddNew"
          >BUAT PROFIL</v-btn>
        </v-card-actions>
      </v-card>
    </v-row>

    <v-row
      class="pa-1"
      v-if="record"
    >
      <v-spacer></v-spacer>
      <v-col :cols="device.desktop ? `12` : `12`">
        <v-card class="animated animate__bounceIn rounded-0">
          <v-card-title :class="`white--text ` + theme.color + ` lighten-1`">
            <v-icon
              small
              color="orange"
              class="mr-2"
            >mdi-circle</v-icon>
            PROFIL PEMDA</v-card-title>
          <v-divider></v-divider>
          <v-tabs
            vertical
            :color="theme.color"
          >
            <v-tab>
              Profil Pemda
            </v-tab>
            <v-tab>
              Indikator
            </v-tab>

            <v-tab-item>
              <v-card flat>
                <v-card-text>
                  <v-row class="">
                    <v-col cols="9">
                      <v-col cols="12">
                        <v-text-field
                          label="Nama Pemerintah"
                          placeholder="Pemerintah Provinsi Banten"
                          :color="theme.color"
                          v-model="record.name"
                          dense
                          outlined
                          hide-details
                        ></v-text-field>
                      </v-col>

                      <v-col cols="12">
                        <v-text-field
                          label="OPD Yang Menangani"
                          :color="theme.color"
                          v-model="record.opd_name"
                          dense
                          outlined
                          hide-details
                          disabled
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12">
                        <v-text-field
                          label="Nama Admin"
                          :color="theme.color"
                          v-model="record.nama_admin"
                          dense
                          outlined
                          hide-details
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12">
                        <v-text-field
                          label="Jabatan Admin"
                          :color="theme.color"
                          v-model="record.jabatan_admin"
                          dense
                          outlined
                          hide-details
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12">
                        <v-text-field
                          label="Nomor Telp"
                          :color="theme.color"
                          v-model="record.phone"
                          dense
                          outlined
                          hide-details
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12">
                        <v-text-field
                          label="Email"
                          :color="theme.color"
                          v-model="record.email"
                          dense
                          outlined
                          hide-details
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12">
                        <v-textarea
                          label="Alamat"
                          :color="theme.color"
                          v-model="record.alamat"
                          dense
                          outlined
                          hide-details
                          rows="3"
                        ></v-textarea>
                      </v-col>
                      <v-col cols="12">
                        <v-text-field
                          label="Fakta Integritas File PDF  (Max: 2 MB)"
                          append-outer-icon="attachment"
                          v-model="filename"
                          :color="theme.color"
                          outlined
                          dense
                          @click:append-outer="uploadFile"
                          hide-details
                        ></v-text-field>
                      </v-col>
                    </v-col>
                    <v-col cols="3">
                      <v-col cols="12">
                        <v-img
                          :class="[theme.color + ' lighten-2 with-backdrop']"
                          :aspect-ratio="3/4"
                          :src="foto"
                          :lazy-src="foto"
                        >
                          <div
                            class="
                                d-flex
                                flex-column
                                align-center
                                justify-center
                                user-select-none
                              "
                            style="height: 100%"
                          >
                            <div class="justify-end justify-content-end">
                              <v-btn
                                icon
                                dark
                                @click="uploadFoto"
                              >
                                <v-icon>photo_camera</v-icon>
                              </v-btn>
                            </div>
                          </div>
                        </v-img>
                        <div class="text-center mt-2">
                          LOGO PEMDA
                        </div>
                      </v-col>
                    </v-col>
                  </v-row>
                </v-card-text>
                <v-card-actions class="mt-5">
                  <v-col class="text-right">
                    <v-btn
                      outlined
                      :color="theme.color"
                      @click="postUpdate"
                    >SIMPAN</v-btn>
                  </v-col>
                </v-card-actions>
              </v-card>
            </v-tab-item>
            <v-tab-item>
              <v-card flat>
                <v-card-text>
                  <v-data-table
                    :headers="indikator.headers"
                    :items="indikator.records"
                    :items-per-page="10"
                    class="elevation-2 mb-1"
                    :color="theme.color"
                    :loading="loading.table"
                    loading-text="Loading... Please wait"
                    :search="search"
                  >
                    <v-progress-linear
                      slot="progress"
                      :color="theme.color"
                      height="1"
                      indeterminate
                    ></v-progress-linear>
                    <template v-slot:item.progress="{ value }">
                      <v-progress-linear
                        :color="theme.color"
                        v-model="value"
                        height="25"
                      >
                        <strong>{{ value }}%</strong>
                      </v-progress-linear>
                    </template>

                    <template v-slot:item.aksi="{ value }">
                      <v-menu
                        bottom
                        origin="center center"
                        transition="scale-transition"
                      >
                        <template v-slot:activator="{ on, attrs }">
                          <v-icon
                            :color="theme.color"
                            v-bind="attrs"
                            v-on="on"
                          >
                            mdi-dots-vertical-circle-outline
                          </v-icon>
                        </template>

                        <v-list>
                          <v-list-item @click="openIndikator(value)">
                            <v-list-item-title>
                              <v-icon
                                class="mr-1"
                                :color="theme.color"
                              >mdi-bullhorn</v-icon>Informasi
                            </v-list-item-title>
                          </v-list-item>
                          <v-list-item @click="openDocument(value)">
                            <v-list-item-title>
                              <v-icon
                                class="mr-1"
                                :color="theme.color"
                              >mdi-file-link</v-icon>Dokumen Pendukung
                            </v-list-item-title>
                          </v-list-item>

                        </v-list>
                      </v-menu>
                    </template>
                  </v-data-table>
                </v-card-text>
              </v-card>
            </v-tab-item>
          </v-tabs>
        </v-card>
      </v-col>
      <v-spacer></v-spacer>
    </v-row>
    <v-col cols="12">
      <v-dialog
        transition="dialog-bottom-transition"
        v-model="indikator.show"
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
            >mdi-circle</v-icon> Formulir Informasi
          </v-toolbar>
          <v-card-text class="mt-2">

            <v-col col="12">
              <v-textarea
                outlined
                :color="theme.color"
                hide-details
                label="*Informasi"
                placeholder=""
                v-model="indikator.record.informasi"
                :filled="indikator.record.informasi"
                rows="4"
                dense
              >{{ indikator.record.informasi }}</v-textarea>
            </v-col>

          </v-card-text>

          <v-divider></v-divider>
          <v-card-actions class="justify-end">
            <v-btn
              outlined
              :color="theme.color"
              @click="postUpdateIndikator"
            >Simpan</v-btn>
            <v-btn
              outlined
              color="grey"
              @click="closeIndikator"
            >Batal</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-col>
  </div>
</template>
    
    <script>
import { mapActions, mapState } from "vuex";
export default {
  name: "profil-pemda",
  data: () => ({
    foto: "/",
    filename: null,
    indikator: {
      headers: [
        {
          text: "INDIKATOR",
          align: "start",
          sortable: true,
          value: "indikator",
        },
        {
          text: "INFORMASI",
          align: "start",
          sortable: true,
          value: "informasi",
        },
        {
          text: "DOK. PENDUKUNG",
          align: "center",
          sortable: true,
          value: "jmldoc",
        },
        {
          text: "AKSI",
          value: "aksi",
          width: 100,
          sortable: false,
          align: "center",
        },
      ],
      records: [],
      record: {},
      show: false,
    },
  }),
  computed: {
    ...mapState([
      "theme",
      "http",
      "device",
      "records",
      "record",
      "loading",
      "event",
      "snackbar",
    ]),
  },
  created() {
    this.setPage({
      crud: true,
      dataUrl: "api/",
      title: "PROFIL PEMDA",
      subtitle: "Manajemen Profil PEMDA",
      breadcrumbs: [
        {
          text: "Permohonan",
          disabled: false,
          href: "",
        },
        {
          text: "Profil PEMDA",
          disabled: false,
          href: "master-jenis-pengaduan",
        },
      ],
      add: false,
      edit: false,
      actions: {
        refresh: true,
        add: true,
        edit: true,
        delete: true,
      },
      showtable: false,
      filename: null,
    });

    this.fetchRecord();
  },
  mounted() {},
  methods: {
    ...mapActions([
      "setPage",
      "assignFileBrowse",
      "getUserInfo",
      "initUploadLibrary",
      "setRecord",
    ]),
    fetchRecord: async function () {
      let { data } = await this.http.get("api/v2/permohonan/profile");
      this.setRecord(data);
      this.foto = data.path_logo;
      this.filename = data.file_fakta_integritas;
      this.fetchIndikator();
    },
    fetchIndikator: async function () {
      try {
        let { data } = await this.http.get(
          "api/v2/permohonan/profile-indikator/" + this.record.id
        );

        this.indikator.records = data;
      } catch (error) {}
    },
    postAddNew: async function () {
      try {
        let {
          data: { code, success, message, error },
        } = await this.http.post("api/v2/permohonan/profile");
        if (!success) {
          this.snackbar.color = "orange";
          this.snackbar.text = message;
          this.snackbar.state = true;
          return;
        }

        this.snackbar.color = this.theme.color;
        this.snackbar.text = message;
        this.snackbar.state = true;
        this.fetchRecord();
      } catch (error) {
        this.snackbar.color = "red";
        this.snackbar.text = "Opps..., terjadi kesalahan";
        this.snackbar.state = true;
      }
    },
    postUpdate: async function () {
      try {
        let {
          data: { code, success, message, error },
        } = await this.http.put(
          "api/v2/permohonan/profile/" + this.record.id,
          this.record
        );

        if (!success) {
          this.snackbar.color = "red";
          this.snackbar.text = message;
          this.snackbar.state = true;
        }

        this.snackbar.color = this.theme.color;
        this.snackbar.text = message;
        this.snackbar.state = true;

        this.fetchRecord();
      } catch (error) {
        this.snackbar.color = "red";
        this.snackbar.text = error.data.errors[0].message;
        this.snackbar.state = true;
      }
    },

    uploadFoto: function () {
      this.assignFileBrowse({
        fileType: [".jpg", ".jpeg", ".png"],
        query: {
          doctype: "documents",
        },
        callback: (response) => {
          setTimeout(() => {
            this.foto = response.path;
            this.record.logo = response.name;
          }, 1000);
        },
      });
    },
    uploadFile: function () {
      this.assignFileBrowse({
        fileType: [".pdf"],
        query: {
          doctype: "documents",
        },
        callback: (response) => {
          setTimeout(() => {
            this.filename = response.name;
            this.record.file_fakta_integritas = response.name;
          }, 500);
        },
      });
    },
    openIndikator: function (val) {
      this.indikator.show = true;
      this.indikator.record.id = val.id;
      this.indikator.record.informasi = val.informasi;
    },
    closeIndikator: function () {
      this.indikator.show = false;
      this.indikator.record = {};
    },
    postUpdateIndikator: async function () {
      try {
        let {
          data: { code, success, message, error },
        } = await this.http.put(
          "api/v2/permohonan/profile-indikator/" +
            this.record.id +
            "/" +
            this.indikator.record.id,
          this.indikator.record
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
        this.closeIndikator();
        this.fetchIndikator();
      } catch (error) {
        this.snackbar.color = "red";
        this.snackbar.text = "Opps..., terjadi kesalahan";
        this.snackbar.state = true;
      }
    },
    openDocument: function (val) {
      this.$router.push({
        name: "permohonan-profile-document",
        params: {
          profile_uuid: val.profile_uuid,
          indikator_pemda_uuid: val.indikator_pemda_uuid,
          profile_indikator_uuid: val.id,
          indikator_pemda_name: val.indikator_pemda_name,
        },
      });
    },
  },
};
</script>
    
    <style></style>
    