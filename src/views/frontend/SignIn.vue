<template>
  <v-app>
    <v-main class="login-background">
      <v-container
        class="fill-height"
        fluid
      >
        <v-row
          align="center"
          justify="center"
        >
          <v-col
            cols="12"
            sm="8"
            md="8"
            :class="device.desktop ? `pa-16`:``"
          >
            <v-card class="elevation-12 animate__animated animate__flipInY">
              <v-window v-model="step">
                <v-window-item :value="1">
                  <v-row>
                    <v-col
                      cols="12"
                      md="8"
                    >
                      <v-card-text class="mt-3">

                        <div class="text-center mt-4">
                          <img
                            src="images/logo.png"
                            alt=""
                            srcset=""
                            :width="device.desktop  ? `200px` : `200px`"
                          >
                        </div>

                        <v-form class="pa-10">
                          <v-text-field
                            label="Email"
                            name="Email"
                            placeholder="exp: admin@tangerangkab.go.id"
                            prepend-icon="email"
                            type="text"
                            color="green darken-1"
                            outlined
                            v-model="uname"
                            dense
                            rounded
                          />

                          <v-text-field
                            id="password"
                            label="Password"
                            name="password"
                            prepend-icon="lock"
                            type="password"
                            color="green darken-1"
                            v-model="upass"
                            outlined
                            dense
                            rounded
                          />

                          <v-row class="justify-center mt-5 pr-5 pl-10">
                            <v-btn
                              rounded
                              :color="theme.color +` darken-2`"
                              dark
                              @click="postAuthent"
                              block
                              large
                            >
                              <v-icon>mdi-login</v-icon>
                              MASUK
                            </v-btn>
                          </v-row>

                        </v-form>
                      </v-card-text>
                    </v-col>
                    <v-col
                      cols="12"
                      md="4"
                      class="green darken-2"
                    >
                      <v-row class="mt-5 mr-5 justify-end">

                      </v-row>
                      <v-card-text
                        class="animate__animated animate__slideInRight animate__delay-1s"
                        :class="device.desktop ? `white--text mt-12`:`white--text mt-5` "
                      >
                        <h3 class="text-center ">PEMPROV BANTEN</h3>
                        <h5 class="text-center">Inovatif, Kratif, Iman dan Taqwa</h5>
                        <div class="mt-5">
                          "Inovasi adalah sinar harapan yang membawa perubahan dan kemajuan dalam dunia ini"
                        </div>

                      </v-card-text>
                    </v-col>
                  </v-row>
                </v-window-item>
                <v-window-item :value="2">
                  <v-row class="fill-height">
                    <v-col
                      cols="12"
                      md="4"
                      class="blue accent-3"
                    >
                      <v-card-text class="white--text mt-12">
                        <h1 class="text-center display-1">Selamat Datang..!</h1>
                        <h5 class="text-center">Untuk Tetap terhubung dengan kami, silakan login dengan info personel Anda</h5>
                      </v-card-text>
                      <div class="text-center">
                        <v-btn
                          rounded
                          outlined
                          dark
                          @click="step--"
                        >Masuk</v-btn>
                      </div>
                    </v-col>

                    <v-col
                      cols="12"
                      md="8"
                    >
                      <v-card-text class="mt-12">
                        <h1 class="text-center display-1 orange--text text--accent-3">Membuat Akun Baru</h1>
                        <div class="text-center mt-4">
                          <v-btn
                            class="mx-2"
                            fab
                            color="blue"
                            outlined
                          >
                            <v-icon>mdi-facebook</v-icon>
                          </v-btn>

                          <v-btn
                            class="mx-2"
                            fab
                            color="orange"
                            outlined
                          >
                            <v-icon>mdi-google</v-icon>
                          </v-btn>
                          <v-btn
                            class="mx-2"
                            fab
                            color="black"
                            outlined
                          >
                            <v-icon>mdi-github</v-icon>
                          </v-btn>
                        </div>
                        <h4 class="text-center mt-4 mb-4">Pastikan email Anda untuk pendaftaran</h4>
                        <v-form class="pa-4">
                          <v-text-field
                            label="Name"
                            name="Name"
                            prepend-icon="person"
                            type="text"
                            color="orange accent-3"
                            outlined
                          />
                          <v-text-field
                            label="Email"
                            name="Email"
                            prepend-icon="email"
                            type="text"
                            color="orange accent-3"
                            outlined
                          />

                          <v-text-field
                            id="password"
                            label="Password"
                            name="password"
                            prepend-icon="lock"
                            type="password"
                            color="orange accent-3"
                            outlined
                          />
                        </v-form>
                      </v-card-text>
                      <div class="text-center mt-n5 mb-5">
                        <v-btn
                          rounded
                          color="orange"
                          dark
                        >SIGN UP</v-btn>
                      </div>
                    </v-col>
                  </v-row>
                </v-window-item>
              </v-window>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
      <v-snackbar
        v-model="snackbar.state"
        :color="snackbar.color"
        :timeout="3500"
        multi-line
      >
        {{ snackbar.text }}

        <template v-slot:action="{ attrs }">
          <v-btn
            :color="theme.color"
            text
            v-bind="attrs"
            @click="snackbarClose"
          >
            Tutup
          </v-btn>
        </template>
      </v-snackbar>
    </v-main>
  </v-app>
</template>

<script>
import { mapActions, mapState } from "vuex";
export default {
  data: () => ({
    step: 1,
    uname: null,
    upass: null,
  }),

  computed: {
    ...mapState([
      "snackbar",
      "theme",
      "thememode",
      "page",
      "device",
      "info",
      "http",
      "auth",
    ]),
  },
  created() {
    this.setPage({
      crud: false,
    }).then(() => {
      this.getAppInfo().then(() => {
        this.getAppInfo().then(() => {
          window.document.title = this.info.app_name;
        });
      });
    });
  },
  mounted() {},
  methods: {
    ...mapActions(["signIn", "getAppInfo", "setPage", "snackbarClose"]),
    postAuthent: function () {
      this.signIn({
        username: this.uname.replace(/ /g, ""),
        userpass: this.upass,
      }).then((pass) => {
        if (!pass) {
          console.clear();
          return;
        }
        try {
          if (this.auth.user.user.authent == "superadmin") {
            this.$router.push({ name: "dashboard" });
          }
          if (this.auth.user.user.authent == "administrator") {
            this.$router.push({ name: "dashboard" });
          }

          if (this.auth.user.user.authent == "operator") {
            this.$router.push({ name: "dashboard" });
          }
        } catch (error) {
          this.snackbar.color = "red";
          this.snackbar.text = error;
          this.snackbar.state = true;
        }
      });
    },
  },
};
</script>
<style>
.bg-image {
  background: url("../../../public/images/innovation.jpeg");
  background-size: 100%;
}
.login-background {
  background: url("../../../public/images/inovasi.jpeg");

  background-origin: content-box;
}
</style>