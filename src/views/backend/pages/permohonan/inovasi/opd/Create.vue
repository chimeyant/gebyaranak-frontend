<template>
  <div :class="device.desktop ? `home pa-6 grey lighten-4`:`home pa-0 grey lighten-4`">

    <v-row class="pa-1">
      <v-spacer></v-spacer>
      <v-col :cols="device.desktop ? `12` : `12`">
        <v-card class="animated animate__fadeIn rounded-0">
          <v-card-title :class="`white--text font-weight-thin ` + theme.color + ` Plighten-1`">
            <v-icon
              small
              color="white"
              class="mr-2"
            >mdi-circle</v-icon>
            Formulir Permohonan Inovasi
          </v-card-title>
          <v-card-text>

            <v-row class="mt-5">
              <v-col cols="12">
                <v-select
                  label="Kategori"
                  outlined
                  dense
                  hide-details
                  v-model="record.category_uuid"
                  :items="categories"
                  :color="theme.color"
                ></v-select>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  class="font-weight-thin"
                  placeholder="Silahkan isi dengan judul inovasi yang anda akan ajukan..."
                  label="Judul Inovasi"
                  outlined
                  dense
                  hide-details
                  :color="theme.color"
                  v-model="record.name"
                  :filled="record.name"
                ></v-text-field>
              </v-col>

              <v-row>
                <v-col cols="6">
                  <v-col cols="12">
                    <v-select
                      label="Jenis Inovasi"
                      class="font-weight-thin"
                      outlined
                      dense
                      hide-details
                      :color="theme.color"
                      v-model="record.jenis_inovasi_uuid"
                      :filled="record.jenis_inovasi_uuid"
                      :items="jenisinovasis"
                    ></v-select>
                  </v-col>
                  <v-col cols="12">
                    <v-select
                      label="Jenis Urusan"
                      class="font-weight-thin"
                      outlined
                      dense
                      hide-details
                      :color="theme.color"
                      v-model="record.urusan_uuid"
                      :filled="record.urusan_uuid"
                      :items="urusans"
                    ></v-select>
                  </v-col>
                  <v-col cols="12">
                    <v-select
                      label="Inisiator"
                      class="font-weight-thin"
                      outlined
                      dense
                      hide-details
                      :color="theme.color"
                      v-model="record.inisiator"
                      :filled="record.inisiator"
                      :items="inisiators"
                    ></v-select>
                  </v-col>
                  <v-col cols="12">
                    <v-select
                      label="Bentuk Inovasi"
                      class="font-weight-thin"
                      outlined
                      dense
                      hide-details
                      :color="theme.color"
                      v-model="record.bentuk_uuid"
                      :filled="record.bentuk_uuid"
                      :items="bentuks"
                    ></v-select>
                  </v-col>
                </v-col>
                <v-col cols="6">
                  <v-col cols="12">
                    <v-text-field
                      class="font-weight-thin"
                      label="Waktu Uji"
                      outlined
                      dense
                      hide-details
                      type="date"
                      :color="theme.color"
                      v-model="record.waktu_uji"
                      :filled="record.waktu_uji"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12">
                    <v-text-field
                      class="font-weight-thin"
                      label="Waktu Penerapan"
                      outlined
                      dense
                      hide-details
                      type="date"
                      :color="theme.color"
                      v-model="record.waktu_penerapan"
                      :filled="record.waktu_penerapan"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12">
                    <v-select
                      label="Tahapan"
                      class="font-weight-thin"
                      outlined
                      dense
                      hide-details
                      :color="theme.color"
                      v-model="record.tahapan"
                      :filled="record.tahapan"
                      :items="tahapans"
                    ></v-select>
                  </v-col>
                  <v-col cols="12">
                    <v-select
                      label="Tahun"
                      class="font-weight-thin"
                      outlined
                      dense
                      hide-details
                      :color="theme.color"
                      v-model="record.tahun"
                      :filled="record.tahun"
                      :items="tahuns"
                    ></v-select>
                  </v-col>
                </v-col>
              </v-row>
              <v-col cols=12>
                <v-textarea
                  label="Rancang Bangun dan Pokok Perubahan yang di lakukan"
                  outlined
                  dense
                  hide-details
                  :color="theme.color"
                  class="font-weight-thin"
                  rows="3"
                  v-model="record.rancang_bangun"
                  :filled="record.rancang_bangun"
                >
                  {{ record.rancang_bangun }}
                </v-textarea>
              </v-col>
              <v-col cols=12>
                <v-textarea
                  label="Tujuan Inovasi Daerah"
                  outlined
                  dense
                  hide-details
                  :color="theme.color"
                  class="font-weight-thin"
                  rows="3"
                  v-model="record.tujuan"
                  :filled="record.tujuan"
                >{{ record.tujuan }}</v-textarea>
              </v-col>
              <v-col cols=12>
                <v-textarea
                  label="Manfaat yang diperoleh"
                  outlined
                  dense
                  hide-details
                  :color="theme.color"
                  class="font-weight-thin"
                  rows="3"
                  v-model="record.manfaat"
                  :filled="record.manfaat"
                >{{ record.manfaat }}</v-textarea>
              </v-col>
              <v-col cols=12>
                <v-textarea
                  label="Hasil inovasi"
                  outlined
                  dense
                  hide-details
                  :color="theme.color"
                  class="font-weight-thin"
                  rows="3"
                  v-model="record.hasil"
                  :filled="record.hasil"
                >{{ record.hasil }}</v-textarea>
              </v-col>
              <v-row>
                <v-col cols="6">
                  <v-col cols="12">
                    <v-text-field
                      label="File Anggaran (PDF | Max: 2Mb)"
                      append-outer-icon="attachment"
                      class="font-weight-thin"
                      v-model="fileanggaran"
                      :filled="fileanggaran"
                      :color="theme.color"
                      outlined
                      dense
                      @click:append-outer="uploadFileAnggaran"
                      hide-details
                    ></v-text-field>
                  </v-col>
                </v-col>
                <v-col cols="6">
                  <v-col cols="12">
                    <v-text-field
                      label="File Profil Bisnis (PDF | Max: 2Mb)"
                      class="font-weight-thin"
                      append-outer-icon="attachment"
                      v-model="fileprofilbisnis"
                      :filled="fileprofilbisnis"
                      :color="theme.color"
                      outlined
                      dense
                      @click:append-outer="uploadFileProfilBisnis"
                      hide-details
                    ></v-text-field>
                  </v-col>
                </v-col>
              </v-row>
              <v-col cols="12">
                <div class="title grey--text">Inovator dan Lokasi Inovasi</div>
              </v-col>
              <v-col cols="12">
                <v-row>
                  <v-col cols="8">
                    <v-text-field
                      class="font-weight-thin"
                      placeholder=""
                      label="Nama Inovator"
                      outlined
                      dense
                      hide-details
                      :color="theme.color"
                      v-model="record.inovator_nama"
                      :filled="record.inovator_nama"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="4">
                    <v-text-field
                      class="font-weight-thin"
                      placeholder=""
                      label="Telp Inovator"
                      outlined
                      dense
                      hide-details
                      :color="theme.color"
                      v-model="record.inovator_phone"
                      :filled="record.inovator_phone"
                    ></v-text-field>
                  </v-col>
                </v-row>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  class="font-weight-thin"
                  placeholder=""
                  label="Nama Instansi"
                  outlined
                  dense
                  hide-details
                  :color="theme.color"
                  v-model="record.inovator_instansi"
                  :filled="record.inovator_instansi"
                ></v-text-field>
              </v-col>
              <v-col cols=12>
                <v-row>
                  <v-col cols="4">
                    <v-select
                      label="Kabupaten/Kota"
                      class="font-weight-thin"
                      outlined
                      dense
                      hide-details
                      :color="theme.color"
                      v-model="record.regency_code"
                      :filled="record.regency_code"
                      :items="regencies"
                      @change="fetchDistricts"
                    ></v-select>
                  </v-col>
                  <v-col cols="4">
                    <v-select
                      label="Kecamatan"
                      class="font-weight-thin"
                      outlined
                      dense
                      hide-details
                      v-model="record.district_code"
                      :filled="record.district_code"
                      :items="districts"
                      :color="theme.color"
                      @change="fetchVillages"
                    ></v-select>
                  </v-col>
                  <v-col cols="4">
                    <v-select
                      label="Desa/Kelurahan"
                      class="font-weight-thin"
                      outlined
                      dense
                      hide-details
                      :color="theme.color"
                      v-model="record.village_code"
                      :filled="record.village_code"
                      :items="villages"
                    ></v-select>
                  </v-col>
                </v-row>
              </v-col>
              <v-col cols=12>
                <v-textarea
                  label="Alamat"
                  outlined
                  dense
                  hide-details
                  :color="theme.color"
                  class="font-weight-thin"
                  rows="2"
                  v-model="record.alamat"
                  :filled="record.alamat"
                >{{ record.alamat }}</v-textarea>
              </v-col>
              <v-col cols=12>
                <v-text-field
                  label="Foto Inovasi (Max: 2Mb)"
                  class="font-weight-thin"
                  append-outer-icon="attachment"
                  v-model="filefoto"
                  :filled="filefoto"
                  :color="theme.color"
                  outlined
                  dense
                  @click:append-outer="uploadFoto"
                  hide-details
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  class="font-weight-thin"
                  placeholder=""
                  label="Video"
                  outlined
                  dense
                  hide-details
                  :color="theme.color"
                  v-model="record.video"
                  :filled="record.video"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  class="font-weight-thin"
                  placeholder=""
                  label="Youtube ID"
                  outlined
                  dense
                  hide-details
                  :color="theme.color"
                  v-model="record.youtube"
                  :filled="record.youtube"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <div class="subtitle-1 grey--text">Alamat Dalam Peta :</div>
              </v-col>
              <v-col cols=12>
                <v-row>
                  <v-col cols="6">
                    <v-img
                      height="100%"
                      width="100%"
                    >

                      <l-map
                        style="height: 300px;width: 100%;z-index:9999; "
                        :zoom="zoom"
                        :center="center"
                        @update:center="centerUpdated"
                      >
                        <v-geosearch
                          :options="geosearchOptions"
                          style="width:100px; border: 1px;"
                        ></v-geosearch>
                        <l-tile-layer
                          :url="url"
                          :attribution="attribution"
                        ></l-tile-layer>
                        <l-marker
                          :key="marker.id"
                          :visible="marker.visible"
                          :draggable="marker.draggable"
                          :lat-lng.sync="marker.position"
                        >

                          <l-icon
                            iconSize=32
                            icon-url="/images/icon-marker-merah.png"
                          />
                          <l-popup :content="marker.tooltip" />
                          <l-tooltip :content="marker.tooltip" />
                        </l-marker>
                      </l-map>
                    </v-img>
                  </v-col>
                  <v-col cols="6">
                    <v-col cols=12>
                      <v-text-field
                        class="font-weight-thin"
                        placeholder="Masukan lokasi.."
                        label="Alamat Dalam Peta"
                        outlined
                        dense
                        hide-details
                        v-model="record.alamat_dalam_peta"
                        :filled="record.alamat_dalam_peta"
                        :color="theme.color"
                      ></v-text-field>
                    </v-col>
                    <v-col cols=12>
                      <v-text-field
                        class="font-weight-thin"
                        placeholder=""
                        label="Garis Bujur"
                        outlined
                        dense
                        hide-details
                        :color="theme.color"
                        v-model="record.lat"
                        :filled="record.lat"
                      ></v-text-field>
                    </v-col>
                    <v-col cols=12>
                      <v-text-field
                        class="font-weight-thin"
                        placeholder=""
                        label="Gari Lintang"
                        outlined
                        dense
                        hide-details
                        :color="theme.color"
                        v-model="record.lng"
                        :filled="record.lng"
                      ></v-text-field>
                    </v-col>
                  </v-col>
                </v-row>
              </v-col>
            </v-row>
          </v-card-text>
          <v-card-actions class="mt-5">
            <v-col class="text-right">
              <v-btn
                outlined
                :color="theme.color"
                @click="postRecord"
              >SIMPAN</v-btn>
              <v-btn
                class="ml-2"
                outlined
                color="grey"
                @click="$router.push({name:'permohonan-inovasi-opd'})"
              >BATAL</v-btn>
            </v-col>
          </v-card-actions>
        </v-card>
      </v-col>
      <v-spacer></v-spacer>
    </v-row>
  </div>
</template>
  
  <script>
import { mapActions, mapState } from "vuex";
import {
  LMap,
  LTileLayer,
  LMarker,
  LIcon,
  LPopup,
  LTooltip,
} from "vue2-leaflet";
import { OpenStreetMapProvider } from "leaflet-geosearch";
import VGeosearch from "vue2-leaflet-geosearch";
import "leaflet/dist/leaflet.css";

export default {
  name: "perusahaan-index",
  components: {
    LMap,
    LTileLayer,
    LMarker,
    VGeosearch,
    LIcon,
    LPopup,
    LTooltip,
  },
  data: () => ({
    foto: "/",
    //map property
    url: "https://tile.openstreetmap.org/{z}/{x}/{y}.png",
    attribution:
      '&copy; <a  class="green--text" target="_blank" href="#">Pemprov Banten</a>',
    zoom: 13,
    //-6.1716001, 106.6405384
    center: [-6.1716001, 106.6405384],

    geosearchOptions: {
      // Important part Here
      provider: new OpenStreetMapProvider(),
    },
    marker: {
      id: "m1",
      position: { lat: -6.1716001, lng: 106.6405384 },
      tooltip: "Pilih lokasi inovasi",
      draggable: true,
      visible: true,
    },

    jenisinovasis: [],
    urusans: [],
    inisiators: [
      { text: "Kepala Daerah", value: "kepala-daerah" },
      { text: "Anggota DPRD", value: "anggota-dprd" },
      { text: "OPD", value: "opd" },
      { text: "ASN", value: "asn" },
      { text: "Masyarakat", value: "masyarakat" },
    ],
    bentuks: [],
    tahapans: [
      { text: "Inisiatif", value: "inisiatif" },
      { text: "Uji Coba", value: "uji-coba" },
      { text: "Penerapan", value: "penerapan" },
    ],
    tahuns: [
      { text: "2024", value: 2024 },
      { text: "2023", value: 2023 },
      { text: "2022", value: 2022 },
      { text: "2021", value: 2021 },
      { text: "2020", value: 2020 },
    ],
    filename: null,
    fileanggaran: null,
    fileprofilbisnis: null,
    filefoto: null,
    regencies: [],
    districts: [],
    villages: [],
    categories: [],
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
      title: "PERMOHONAN",
      subtitle: "Formulir Permohonan Inovasi",
      breadcrumbs: [
        {
          text: "Permohonan",
          disabled: true,
          href: "",
        },
        {
          text: "Inovasi",
          disabled: true,
          href: "#",
        },
        {
          text: "Formulir",
          disabled: false,
          href: "#",
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
    });

    //this.fetchRecord();
  },
  mounted() {
    this.fetchJenisInovasi();
    this.fetchUrusans();
    this.fetchBentuks();
    this.fetchRegencies();
    this.fetchCategories();
  },
  methods: {
    ...mapActions([
      "setPage",
      "assignFileBrowse",
      "getUserInfo",
      "initUploadLibrary",
      "setRecord",
    ]),
    fetchRecord: async function () {
      let { data } = await this.http.get("api/v2/user-info");

      this.setRecord(data);

      this.foto = data.avatar_path;
    },
    postRecord: async function () {
      try {
        let {
          data: { success, message },
        } = await this.http.post("api/v2/permohonan/opd/inovasi", this.record);

        if (!success) {
          this.snackbar.color = "red";
          this.snackbar.text = message;
          this.snackbar.state = true;
        }

        this.snackbar.color = this.theme.color;
        this.snackbar.text = message;
        this.snackbar.state = true;

        this.$router.push({ name: "permohonan-inovasi-opd" });
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
            this.filefoto = response.name;
            this.record.foto = response.name;
          }, 1000);
        },
      });
    },
    uploadFileAnggaran: function () {
      this.assignFileBrowse({
        fileType: [".pdf"],
        query: {
          doctype: "documents",
        },
        callback: (response) => {
          setTimeout(() => {
            this.fileanggaran = response.name;
            this.record.file_anggaran = response.name;
          }, 500);
        },
      });
    },
    uploadFileProfilBisnis: function () {
      this.assignFileBrowse({
        fileType: [".pdf"],
        query: {
          doctype: "documents",
        },
        callback: (response) => {
          setTimeout(() => {
            this.fileprofilbisnis = response.name;
            this.record.file_profil_bisnis = response.name;
          }, 500);
        },
      });
    },
    centerUpdated(center) {
      this.center = center;
    },
    getUserPosition: async function () {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition((pos) => {
          this.center = { lat: pos.coords.latitude, lng: pos.coords.longitude };
          this.center = [pos.coords.latitude, pos.coords.longitude];
          this.marker.position = {
            lat: pos.coords.latitude,
            lng: pos.coords.longitude,
          };
        });
      }
    },
    fetchJenisInovasi: async function () {
      try {
        let { data } = await this.http.get("api/v2/combo/jenis-inovasi");
        this.jenisinovasis = data;
      } catch (error) {}
    },
    fetchUrusans: async function () {
      try {
        let { data } = await this.http.get("api/v2/combo/urusan");
        this.urusans = data;
      } catch (error) {}
    },
    fetchBentuks: async function () {
      try {
        let { data } = await this.http.get("api/v2/combo/bentuk");
        this.bentuks = data;
      } catch (error) {}
    },
    fetchRegencies: async function () {
      try {
        let { data } = await this.http.get("api/v2/combo/regency");
        this.regencies = data;
      } catch (error) {}
    },
    fetchDistricts: async function () {
      try {
        let { data } = await this.http.get(
          "api/v2/combo/district/" + this.record.regency_code
        );
        this.districts = data;
      } catch (error) {}
    },
    fetchVillages: async function () {
      try {
        let { data } = await this.http.get(
          "api/v2/combo/village/" + this.record.district_code
        );
        this.villages = data;
      } catch (error) {}
    },
    fetchCategories: async function () {
      try {
        let { data } = await this.http.get("api/v2/combo/category");
        this.categories = data;
      } catch (error) {}
    },
  },
  watch: {
    "marker.position": {
      handler() {
        this.record.lat = this.marker.position.lat;
        this.record.lng = this.marker.position.lng;
      },
      deep: true,
    },
  },
};
</script>
  
  <style></style>
  