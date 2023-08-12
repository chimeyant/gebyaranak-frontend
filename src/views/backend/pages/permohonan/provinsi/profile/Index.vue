<template>
  <div :class="device.desktop ? `home pa-6 grey lighten-4`:`home pa-0 grey lighten-4`">
    <v-row>

    </v-row>

    <v-row class="pa-1">
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
                          label="Nama"
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
                          v-model="record.nama_admin"
                          dense
                          outlined
                          hide-details
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12">
                        <v-text-field
                          label="OPD Yang Menangani"
                          :color="theme.color"
                          v-model="record.nama_admin"
                          dense
                          outlined
                          hide-details
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12">
                        <v-text-field
                          label="Nomor Telp"
                          :color="theme.color"
                          v-model="record.nama_admin"
                          dense
                          outlined
                          hide-details
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12">
                        <v-text-field
                          label="Email"
                          :color="theme.color"
                          v-model="record.nama_admin"
                          dense
                          outlined
                          hide-details
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12">
                        <v-textarea
                          label="Alamat"
                          :color="theme.color"
                          v-model="record.nama_admin"
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
                          LOGO
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
                      @click="fetchUpdate"
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
                  </v-data-table>
                </v-card-text>
              </v-card>
            </v-tab-item>
          </v-tabs>
        </v-card>
      </v-col>
      <v-spacer></v-spacer>
    </v-row>
  </div>
</template>
  
  <script>
import { mapActions, mapState } from "vuex";
export default {
  name: "profil-pemda",
  data: () => ({
    foto: "/",
    indikator: {
      headers: [
        {
          text: "#",
          align: "start",
          sortable: true,
          value: "nom",
          width: 150,
        },
        {
          text: "INDIKATOR",
          align: "start",
          sortable: true,
          value: "name",
        },
        {
          text: "INFORMASI",
          align: "start",
          sortable: true,
          value: "name",
        },
        {
          text: "JML.DOK",
          align: "start",
          sortable: true,
          value: "name",
        },
        {
          text: "AKSI",
          value: "id",
          width: 100,
          sortable: false,
          align: "center",
        },
      ],
      records: [],
      record: {},
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
      this.foto = data.avatar_path;
    },
    fetchUpdate: async function () {
      try {
        let {
          data: { success, message },
        } = await this.http.post("api/v2/utility/update-profil", this.record);

        if (!success) {
          this.snackbar.color = "red";
          this.snackbar.text = message;
          this.snackbar.state = true;
        }

        this.snackbar.color = this.theme.color;
        this.snackbar.text = message;
        this.snackbar.state = true;

        this.fetchRecord();
        this.getUserInfo();
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
          doctype: "avatars",
        },
        callback: (response) => {
          setTimeout(() => {
            this.foto = response.path;
            this.record.avatar = response.name;
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
            this.record.filename = response.name;
          }, 500);
        },
      });
    },
  },
};
</script>
  
  <style></style>
  