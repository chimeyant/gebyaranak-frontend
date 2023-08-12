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
          <div class="subtitle-1 font-weight-bold">Pemeberitahuan</div>
        </v-row>

        <v-card-text class="mb-2">
          Selamat proses registrasi anda berhasil..!, untuk melihat sertifikat anda silahkan lihat pada folder unduhan pada perangkat anda.
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
                @click="$router.push({name:'home'})"
              >Kembali</v-btn>
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




