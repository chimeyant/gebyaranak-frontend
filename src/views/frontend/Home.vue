<template>
  <div style="background-image: url('images/merahputih.jpeg');height: 100%;">

    <div style="display: flex ; justify-content: center; align-items: center; height: 100vh; ">

      <v-card
        :width="device.desktop ? 450:'98%'"
        class="animate__animated animate__fadeInUp mt-5"
      >
        <v-row class="mt-5 justify-center mb-7">
          <img
            src="images/logo78.png"
            alt=""
            height="76"
            width="76"
          >
        </v-row>
        <v-row class="justify-center mb-3">
          <div class="subtitle-1 font-weight-bold">Formulir Daftar Peserta Gebyar Anak</div>
        </v-row>
        <v-row class="justify-center mb-2">
          <div class="subtitle-1 font-weight-bold">Provinsi Banten</div>
        </v-row>
        <v-card-text class="mb-2">
          <v-row>
            <v-col cols="12">
              <v-text-field
                label="Nama Peserta"
                outlined
                dense
                hide-details
                color="red"
                v-model="record.name"
              ></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-text-field
                label="Asal Sekolah"
                outlined
                dense
                hide-details
                color="red"
                v-model="record.asal_sekolah"
              ></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-select
                label="Lembaga Pendidikan"
                outlined
                dense
                hide-details
                color="red"
                :items="lembagas"
                v-model="record.lembaga"
              ></v-select>
            </v-col>
            <v-col cols="12">
              <v-select
                label="Lomba yang diikuti"
                outlined
                dense
                hide-details
                color="red"
                :items="lombas"
                v-model="record.lomba"
              ></v-select>
            </v-col>
            <v-col cols="12">
              <v-text-field
                label="Nomor HP (Whatsapp)"
                placeholder="0812XXX"
                outlined
                dense
                hide-details
                color="red"
                type="number"
                v-model="record.phone"
              ></v-text-field>
            </v-col>
          </v-row>
        </v-card-text>
        <v-card-actions>
          <v-row class="justify-end pa-2 mb-5">
            <v-col cols="12">
              <v-btn
                outlined
                color="red"
                block
                dense
                hide-details
                @click="postRegister"
              >Kirim</v-btn>
            </v-col>
            <v-col
              cols="12"
              v-show="false"
            >
              <v-btn
                color="red"
                block
                dense
                hide-details
                class="white--text"
              >Cetak Ulang</v-btn>
            </v-col>
          </v-row>
        </v-card-actions>
        <v-row class="pa-5 justify-center">
          <div
            style="font-size: 8pt;"
            class="grey--text"
          >Provinsi Banten copyright &copy; 2023 </div>
        </v-row>
      </v-card>
    </div>
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";

export default {
  name: "home",
  components: {},
  data: () => ({
    lembagas: [
      { text: "Taman Kanak-Kanak", value: "TK" },
      { text: "Kelompok Bermain", value: "KB" },
      { text: "Raudhatul Athfal ", value: "RA" },
    ],
    lombas: [
      { text: "Menyanyi", value: "menyanyi" },
      { text: "Menyusun Balok", value: "menyusun-balok" },
      { text: "Estafet Benderak", value: "estafet-bendera" },
      { text: "Gerak & Lagu", value: "gerak-dan-lagu" },
      { text: "Bercerita", value: "bercerita" },
      { text: "Hafalan Surat", value: "hafalan-surat" },
    ],
    record: {},
  }),
  mounted() {
    this.setPage({
      name: "home",
      crud: false,
    });
  },
  computed: {
    ...mapState([
      "device",
      "theme",
      "info",
      "snackbar",
      "loading",
      "page",
      "http",
    ]),
  },
  methods: {
    ...mapActions(["setPage", "getAppInfo", "snackbarClose", "catchError"]),
    postRegister: async function () {
      try {
        let {
          data: { code, success, message, path_download },
        } = await this.http.post("api/v2/register-peserta", this.record);
        if (!success) {
          this.snackbar.color = "red";
          this.snackbar.text = message;
          this.snackbar.state = true;
          return;
        }
        this.snackbar.color = "green";
        this.snackbar.text = message;
        this.snackbar.state = true;
        window.open(path_download, "__BLANK");
        this.$router.push({ name: "registrasi-berhasil" });
        this.record = {};
      } catch (error) {
        this.snackbar.color = "red";
        this.snackbar.text = "Opps..., terjadi kesalahan";
        this.snackbar.state = true;
      }
    },
  },
};
</script>




