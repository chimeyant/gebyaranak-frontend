<template>
  <div :class="device.desktop ? `home pa-6`:`home pa-0`">
    <v-row>
      <v-col :cols="device.desktop ? `12` : `12`">
        <v-card class="animated animate__bounceIn rounded-0">
          <v-card-title :class="`flex flex-row-reverse ` + theme.color + ` lighten-1`">
            <v-tooltip
              :color="theme.color + ` draken-4`"
              bottom
            >
              <template v-slot:activator="{ on }">
                <v-btn
                  text
                  small
                  icon
                  v-on="on"
                  class="animate__animated animate__shakeY animate__delay-1s"
                >
                  <v-icon
                    color="white"
                    @click="openForm"
                  >add_circle</v-icon>
                </v-btn>
              </template>
              <span>Tambah Slider</span>
            </v-tooltip>

            <v-tooltip
              :color="theme.color + ` draken-4`"
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
                    color="white"
                    @click="fetchRecords"
                  >mdi-refresh-circle</v-icon>
                </v-btn>
              </template>
              <span>Refresh</span>
            </v-tooltip>

            <v-spacer></v-spacer>
            <v-text-field
              v-model="search"
              append-icon="mdi-magnify"
              label="Pencarian"
              single-line
              hide-details
              dense
              solo
              :color="theme.color"
            ></v-text-field>
          </v-card-title>
          <v-data-table
            v-show="device.desktop"
            :headers="headers"
            :items="records"
            :items-per-page="table.options.itemsPerPage"
            :page.sync="table.options.page"
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
            <template v-slot:item.logo="{ value }">
              <img
                class="pa-2"
                :src="value"
                alt=""
                srcset=""
                width="75"
                height="75"
              >
            </template>
            <template v-slot:item.status="{ value }">
              <v-chip
                small
                :color="value ? 'green' : 'red'"
              >{{ value ? 'AKTIF': 'NON AKTIF'}}</v-chip>
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
                  <v-list-item @click="editRecord(value)">
                    <v-list-item-title>
                      <v-icon color="orange">mdi-pencil-circle</v-icon>
                      Ubah Data
                    </v-list-item-title>
                  </v-list-item>
                  <v-list-item @click="postDeleteRecord(value)">
                    <v-list-item-title>
                      <v-icon color="red">mdi-delete-circle</v-icon>
                      Hapus Data
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
                v-for="item in records"
                :key="item.id"
              >
                <template v-slot:default="{ active }">
                  <v-list-item-action>
                    <v-checkbox :input-value="active"></v-checkbox>
                  </v-list-item-action>
                  <v-list-item-content>
                    <v-list-item-title>{{ item.title }}</v-list-item-title>
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
                        <v-list-item @click="editRecord(item.id)">
                          <v-list-item-title>
                            <v-icon color="orange">mdi-pencil-circle</v-icon>
                            Edit
                          </v-list-item-title>
                        </v-list-item>
                        <v-list-item @click="postDeleteRecord(item.id)">
                          <v-list-item-title>
                            <v-icon color="red">mdi-delete-circle</v-icon>
                            Hapus
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
    <v-col col="12">
      <v-dialog
        transition="dialog-bottom-transition"
        v-model="form.add"
        :max-width="device.desktop ? `600px` : `100%`"
        persistent
        :fullscreen="device.mobile"
      >
        <v-card class="rounded-0">
          <v-toolbar
            :color="theme.color"
            dark
          >
            <v-icon
              small
              color="orange"
              class="mr-1 animate__animated animate__flash animate__infinite"
            >mdi-circle</v-icon>Formulir Instansi Pendukung
          </v-toolbar>
          <v-card-title class="justify-center">FORMULIR INSTANSI PENDUKUNG</v-card-title>
          <v-card-text>
            <v-row :no-gutters="device.mobile">
              <v-col cols="12">
                <v-text-field
                  label="Nama Instansi"
                  :color="theme.color"
                  :hide-details="device.desktop"
                  autocomplete="off"
                  v-model="record.name"
                  outlined
                  :dense="device.desktop"
                >
                </v-text-field>
              </v-col>

              <v-col cols=12>
                <v-text-field
                  label="Logo Max: 2Mb"
                  append-outer-icon="attachment"
                  v-model="logo"
                  :color="theme.color"
                  outlined
                  dense
                  @click:append-outer="uploadLogo"
                  hide-details
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  label="Website/Url"
                  :color="theme.color"
                  :hide-details="device.desktop"
                  autocomplete="off"
                  v-model="record.website"
                  outlined
                  :dense="device.desktop"
                >
                </v-text-field>
              </v-col>
              <v-col cols="12">
                <v-row>
                  <v-col cols="6">
                    <v-switch
                      label="Publish"
                      :color="theme.color"
                      v-model="record.status"
                      :hide-details="device.desktop"
                    ></v-switch>
                  </v-col>
                </v-row>
              </v-col>
            </v-row>
          </v-card-text>
          <v-card-actions class="flex flex-row-reverse">
            <v-btn
              outlined
              :color="theme.color"
              @click="postAddNewRecord"
              v-show="!form.edit"
            >TAMBAH</v-btn>
            <v-btn
              outlined
              :color="theme.color"
              @click="postUpdateRecord"
              v-show="form.edit"
            >UBAH</v-btn>
            <v-btn
              outlined
              class="mr-2"
              color="grey dark-3"
              @click="closeForm"
            >BATAL</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-col>
  </div>
</template>
  
  <script>
import { mapActions, mapState } from "vuex";

export default {
  name: "sponsor",
  data: () => ({
    num: 1,

    headers: [
      {
        text: "LOGO",
        align: "center",
        sortable: false,
        value: "logo",
        width: 100,
      },
      {
        text: "INSTANSI | ORGANISASI",
        align: "start",
        sortable: false,
        value: "name",
      },
      {
        text: "PUBLISH",
        value: "status",
        sortable: false,
        width: 100,
        align: "center",
      },
      { text: "AKSI", value: "id", sortable: false, width: 50 },
    ],
    status: [
      { text: "Aktif", value: 0 },
      { text: "Non Aktif", value: 1 },
    ],

    search: null,
    logo: null,

    add: false,
    edit: false,
  }),
  computed: {
    ...mapState([
      "theme",
      "http",
      "device",
      "record",
      "records",
      "loading",
      "event",
      "table",
      "form",
      "corlib",
    ]),
  },
  created() {
    this.setPage({
      crud: true,
      dataUrl: "api/v2/halaman-depan/sponsor",
      pagination: false,
      title: "INSTANSI PENDUKUNG",
      subtitle: "Berikut Daftar Seluruh Instansi Pendukung Yang Tersedia",
      breadcrumbs: [
        {
          text: "Halaman Depan",
          disabled: false,
          href: "",
        },
        {
          text: "Pendukung",
          disabled: false,
          href: "",
        },
      ],
      showtable: true,
    });
    this.fetchRecords();
  },
  mounted() {},
  methods: {
    ...mapActions([
      "setPage",
      "fetchRecords",
      "postAddNew",
      "postEdit",
      "postUpdate",
      "postConfirmDelete",
      "assignFileBrowse",
      "setForm",
    ]),
    openForm: function () {
      this.setForm({
        add: true,
        edit: false,
      });
      this.foto = "/";
      this.top_image = null;
      this.bottom_image = null;
    },
    closeForm: function () {
      this.setForm({
        add: false,
        edit: false,
      });
    },
    postAddNewRecord: function () {
      this.postAddNew(this.record).then(() => {
        this.fetchRecords();
        this.closeForm();
      });
    },
    editRecord: function (val) {
      this.postEdit(val).then(() => {
        this.foto = this.record.path_url;
        this.top_image = this.record.top_image;
        this.bottom_image = this.record.bottom_image;
      });
      this.setForm({
        add: true,
        edit: true,
      });
    },

    postUpdateRecord: function () {
      this.postUpdate(this.record).then(() => {
        this.fetchRecords();
        this.add = false;
        this.edit = false;
        this.closeForm();
      });
    },

    postDeleteRecord: function (val) {
      this.postConfirmDelete(val);
    },

    uploadLogo: function () {
      this.assignFileBrowse({
        fileType: [".jpg", ".jpeg", ".png"],
        query: {
          doctype: "sliders",
        },
        callback: (response) => {
          setTimeout(() => {
            this.logo = response.name;
            this.record.logo = response.name;
          }, 1000);
        },
      });
    },
  },
};
</script>
  