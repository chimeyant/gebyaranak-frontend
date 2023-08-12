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
                >
                  <v-icon
                    :color="theme.mode == 'dark' ? `white` : `black`"
                    @click="fetchRecords"
                  >refresh</v-icon>
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
                  class=""
                >
                  <v-icon
                    :color="theme.mode == 'dark' ? `white` : `black`"
                    @click="openFormImport"
                  >mdi-file-excel</v-icon>
                </v-btn>
              </template>
              <span>Upload Data</span>
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
                  v-show="page.actions.add"
                  class="animate__animated animate__shakeY animate__delay-1s"
                >
                  <v-icon
                    :color="theme.mode == 'dark' ? `white` : `black`"
                    @click="openForm"
                  >add_circle</v-icon>
                </v-btn>
              </template>
              <span>Tambah Data</span>
            </v-tooltip>

            <v-spacer></v-spacer>
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
          </v-card-title>
          <v-data-table
            v-show="device.desktop"
            :headers="headers"
            :items="records"
            :items-per-page="table.options.itemsPerPage"
            :page.sync="table.footer.page"
            class="elevation-2 mb-1"
            :color="theme.color"
            :loading="loading.table"
            loading-text="Loading... Please wait"
            :search="search"
            hide-default-footer
            @page-count="table.options.pageCount = $event"
            show-select
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

            <template v-slot:item.nama_pasien="{ value }">
              <span
                class="red--text font-weight-bold"
                v-show="!value.status"
              >{{ value.text }}</span>
              <span
                class="black--text"
                v-show="value.status"
              >{{ value.text }}</span>
            </template>

            <template v-slot:item.kategori="{ value }">
              <v-select
                label="Pilih Kategori"
                outlined
                dense
                hide-details
                :items="categories"
                v-model="value.category_uuid"
                @change="postCategory(value)"
                :color="theme.color"
              ></v-select>
            </template>

            <template v-slot:item.pengobatan="{ value }">
              <v-chip
                small
                :color="value.color"
                class="white--text"
              >{{ value.text }}</v-chip>
            </template>

            <template v-slot:item.status="{ value }">
              <v-select
                label="Pilih Status"
                outlined
                dense
                hide-details
                :color="theme.color"
                v-model="value.status"
                :items="statuses"
                @change="postStatus(value)"
              ></v-select>
            </template>
            <template v-slot:item.id="{ value }">
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
                  <v-list-item
                    @click="editRecord(value)"
                    v-show="page.actions.edit"
                  >
                    <v-list-item-title>
                      <v-icon color="orange">mdi-pencil-circle</v-icon>Ubah
                    </v-list-item-title>
                  </v-list-item>
                  <v-list-item
                    @click="postDeleteRecord(value)"
                    v-show="page.actions.delete"
                  >
                    <v-list-item-title>
                      <v-icon color="red">mdi-delete-circle</v-icon>Hapus
                    </v-list-item-title>
                  </v-list-item>
                </v-list>
              </v-menu>
            </template>
          </v-data-table>
          <v-list
            subheader
            v-show="device.mobile"
          >

            <v-list-item-group
              multiple
              active-class=""
            >
              <v-list-item
                v-for="item in filterItems"
                :key="item.id"
                style="border: ;1px solid"
              >
                <template v-slot:default="{ active }">
                  <v-list-item-action>
                    <v-checkbox :input-value="active"></v-checkbox>
                  </v-list-item-action>
                  <v-list-item-content>
                    <v-list-item-title>{{ item.name }}</v-list-item-title>
                    <v-list-item-subtitle>{{ item.description }} </v-list-item-subtitle>
                  </v-list-item-content>
                  <v-list-item-action>
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

                        <v-divider v-if="page.delete || page.edit"></v-divider>
                        <v-list-item
                          @click="editRecord(item.id)"
                          v-show="page.actions.edit"
                        >
                          <v-list-item-title>
                            <v-icon color="orange">mdi-pencil-circle</v-icon>
                            Ubah Data
                          </v-list-item-title>
                        </v-list-item>
                        <v-list-item
                          @click="postDeleteRecord(item.uuid)"
                          v-show="page.actions.delete"
                        >
                          <v-list-item-title>
                            <v-icon color="red">mdi-delete-circle</v-icon>
                            Hapus Data
                          </v-list-item-title>
                        </v-list-item>
                      </v-list>
                    </v-menu>
                  </v-list-item-action>
                </template>
              </v-list-item>
            </v-list-item-group>
          </v-list>
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
            >mdi-circle</v-icon> Formulir Data Klaim
          </v-toolbar>
          <v-card-text class="mt-2">
            <v-col col="12">
              <v-text-field
                outlined
                :color="theme.color"
                hide-details
                label="Nama Pasien"
                placeholder=""
                v-model="record.nama_pasien"
                :filled="record.nama_pasien"
                dense
              ></v-text-field>
            </v-col>
            <v-col col="12">
              <v-text-field
                outlined
                :color="theme.color"
                hide-details
                label="Umur"
                placeholder=""
                v-model="record.umur"
                :filled="record.umur"
                dense
              ></v-text-field>
            </v-col>
            <v-col cols=12>
              <v-select
                label="Kelas BPSJ"
                outlined
                dense
                hide-details
                :color="theme.color"
                v-model="record.bpjs_kelas_uuid"
                :items="kelasbpjs"
              ></v-select>
            </v-col>
            <v-col cols=12>
              <v-textarea
                label="Keterangan Pending"
                outlined
                dense
                hide-details
                v-model="record.description"
                rows="3"
              >{{ record.description }}</v-textarea>
            </v-col>
            <v-col cols="12">
              <v-autocomplete
                label="Dokter"
                outlined
                dense
                hide-details
                :color="theme.color"
                :items="doctors"
                v-model="record.doctor_uuid"
              ></v-autocomplete>
            </v-col>
            <v-col cols=12>
              <v-select
                label="Kategori"
                outlined
                dense
                hide-details
                :color="theme.color"
                v-model="record.category_uuid"
                :items="categories"
              ></v-select>
            </v-col>
            <v-col col="12">
              <v-text-field
                outlined
                :color="theme.color"
                hide-details
                label="Total Tarif"
                placeholder=""
                v-model="record.total_tarif"
                :filled="record.total_tarif"
                dense
              ></v-text-field>
            </v-col>
            <v-col col="12">
              <v-text-field
                outlined
                :color="theme.color"
                hide-details
                label="Tarif Rumah Sakit"
                placeholder=""
                v-model="record.tarif_rs"
                :filled="record.tarif_rs"
                dense
              ></v-text-field>
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
        v-model="formimport.show"
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
            >mdi-circle</v-icon> Formulir Upload Data Klaim
          </v-toolbar>
          <v-card-text class="mt-2">
            <v-col cols="12">
              <v-text-field
                label="File Data Klaim (XLSX)"
                append-outer-icon="attachment"
                v-model="formimport.fileName"
                :color="theme.color"
                outlined
                dense
                @click:append-outer="uploadFile"
                hide-details
              ></v-text-field>
            </v-col>
            <v-col col="12">
              <v-select
                label="Bulan"
                outlined
                dense
                hide-details
                :color="theme.color"
                v-model="formimport.sheetName"
                :items="bulans"
              ></v-select>
            </v-col>
            <v-col col="12">
              <v-select
                label="Jenis Pengobatan"
                outlined
                dense
                hide-details
                :color="theme.color"
                v-model="formimport.jenisPengobatan"
                :items="jenispengobatans"
              ></v-select>
            </v-col>
          </v-card-text>

          <v-divider></v-divider>
          <v-card-actions class="justify-end">
            <v-btn
              outlined
              :color="theme.color"
              v-show="!form.edit"
              @click="postImport"
            >Proses Import</v-btn>

            <v-btn
              outlined
              color="grey"
              @click="closeFormImport"
            >Batal</v-btn>
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
  name: "master-diagnosis",
  data: () => ({
    num: 1,
    headers: [
      {
        text: "NAMA PASIEN",
        align: "start",
        sortable: false,
        width: 250,
        value: "nama_pasien",
      },
      {
        text: "TANGGAL",
        value: "discharge_date",
        sortable: false,
        align: "center",
        width: 100,
      },
      {
        text: "KATEGORI",
        value: "kategori",
        sortable: false,
        align: "center",
        width: 250,
      },
      {
        text: "KET. PENDING",
        value: "description",
        sortable: false,
        align: "left",
        width: 300,
      },
      {
        text: "DOKTER",
        value: "doctor",
        sortable: false,
        align: "left",
        width: 300,
      },
      {
        text: "PENGOBATAN",
        value: "pengobatan",
        sortable: false,
        align: "left",
        width: 100,
      },
      {
        text: "TOTAL TARIF",
        value: "total_tarif",
        sortable: false,
        align: "right",
      },
      {
        text: "TARIF RS",
        value: "tarif_rs",
        sortable: false,
        align: "right",
      },
      {
        text: "STATUS",
        value: "status",
        sortable: false,
        align: "center",
        width: 250,
      },

      {
        text: "AKSI",
        value: "id",
        width: 80,
        sortable: false,
        align: "center",
      },
    ],
    search: null,
    filename: null,
    formimport: {
      show: false,
      fileName: null,
      sheetName: null,
      jenisPengobatan: null,
    },
    doctors: [],
    categories: [],
    category_uuid: null,
    bulans: [
      { text: "JANUARI", value: "JANUARI" },
      { text: "PERBRUARI", value: "PEBRUARI" },
      { text: "MARET", value: "MARET" },
      { text: "APRIL", value: "APRIL" },
      { text: "MEI", value: "MEI" },
      { text: "JUNI", value: "JUNI" },
      { text: "JULI", value: "JULI" },
      { text: "AGUSTUS", value: "AGUSTUS" },
      { text: "SEPTEMBER", value: "SEPTEMBER" },
      { text: "OKTOBER", value: "OKTOBER" },
      { text: "NOPEMBER", value: "NOPEMBER" },
      { text: "DESEMBER", value: "DESEMBER" },
    ],
    kelasbpjs: [],
    statuses: [
      { text: "Belum Terverifikasi", value: false },
      { text: "Sudah Terverifikasi", value: true },
    ],
    jenispengobatans: [
      { text: "Rawat Jalan", value: true },
      { text: "Rawat Inap", value: false },
    ],
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
      dataUrl: "api/v2/manajemen/klaim",
      pagination: true,
      key: "id",
      title: "MANAJEMEN KLAIM",
      subtitle: "Berikut Daftar Seluruh Klaim Yang Tersedia",

      breadcrumbs: [
        {
          text: "Manajemen",
          disabled: true,
          href: "",
        },
        {
          text: "Klaim",
          disabled: true,
          href: "",
        },
      ],
      showtable: true,
      actions: {
        refresh: true,
        add: false,
        edit: true,
        delete: true,
        bulkdelete: false,
        print: false,
        export: false,
        help: false,
      },
    });

    this.fetchRecords();
  },
  mounted() {
    this.setTable({
      options: {
        page: 1,
      },
    });
    this.fetchCategories();
    this.fetchKelasBpjs();
    this.fetchDoctors();
  },
  methods: {
    ...mapActions([
      "setPage",
      "fetchRecords",
      "postAddNew",
      "postEdit",
      "postUpdate",
      "postConfirmDelete",
      "assignFileBrowse",
      "setLoading",
      "setRecord",
      "setForm",
      "setTable",
    ]),
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
        fileType: [".xls", ".xlsx"],
        query: {
          doctype: "documents",
        },
        callback: (response) => {
          setTimeout(() => {
            this.formimport.fileName = response.name;
            // this.record.icon = response.name;
            this.snackbar.color = this.theme.color;
            this.snackbar.text = "Proses upload file berhasil...!";
            this.snackbar.state = true;
          }, 500);
        },
      });
    },
    openFormImport: function () {
      this.formimport.show = true;
      this.formimport.sheetName = "";
      this.formimport.fileName = "";
    },
    closeFormImport: function () {
      this.formimport.show = false;
      this.formimport.sheetName = "";
      this.formimport.fileName = "";
    },
    postImport: async function () {
      try {
        this.setLoading({ dialog: true, text: "Proses import data...!" });
        let {
          data: { code, success, message },
        } = await this.http
          .post("api/v2/manajemen/klaim-import", {
            filename: this.formimport.fileName,
            sheetName: this.formimport.sheetName,
            jenisPengobatan: this.formimport.jenisPengobatan,
          })
          .then(() => {
            this.fetchRecords();
            this.closeFormImport();
          });
      } catch (error) {
      } finally {
        this.setLoading({ dialog: false, text: "" });
      }
    },
    fetchCategories: async function () {
      try {
        let { data } = await this.http.get("api/v2/combo/category");
        this.categories = data;
      } catch (error) {}
    },
    postCategory: async function (val) {
      try {
        this.setLoading({ dialog: true, text: "Proses ubah kategori" });
        let {
          data: { code, success, message, error },
        } = await this.http.post("api/v2/manajemen/klaim-update-category", {
          category_uuid: val.category_uuid,
          id: val.id,
        });
        if (!success) {
          this.snackbar.color = "red";
          this.snackbar.text = message;
          this.snackbar.state = true;
          return;
        }

        this.snackbar.color = this.theme.color;
        this.snackbar.text = message;
        this.snackbar.state = true;
      } catch (error) {
        this.snackbar.color = "red";
        (this.snackbar.text = "Opps..., terjadi kesalahan "),
          (this.snackbar.state = true);
      } finally {
        this.setLoading({ dialog: false, text: false });
      }
    },
    fetchKelasBpjs: async function () {
      try {
        let { data } = await this.http.get("api/v2/combo/kelas-bpjs");
        this.kelasbpjs = data;
      } catch (error) {}
    },
    fetchDoctors: async function () {
      try {
        let { data } = await this.http.get("api/v2/combo/dokter");
        this.doctors = data;
      } catch (error) {}
    },
    postStatus: async function (val) {
      try {
        this.setLoading({ dialog: true, text: "Proses ubah status" });
        let {
          data: { code, success, message, error },
        } = await this.http.post("api/v2/manajemen/klaim-update-status", {
          status: val.status,
          id: val.id,
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
      } catch (error) {
        this.snackbar.color = "red";
        this.snackbar.text = "Opps..., terjadi kesalahan ";
        this.snackbar.state = true;
      } finally {
        this.setLoading({ dialog: false, text: "" });
      }
    },
  },
  watch: {
    "table.options": {
      handler() {
        this.fetchRecords();
      },
      deep: true,
    },
  },
};
</script>