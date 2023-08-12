<template>
  <div>
    <v-container>
      <v-row class="justify-center mt-8">
        <v-col :cols="device.desktop ? 12:12">
          <h2
            v-show="device.desktop"
            class=" topik-title animate__animated animate__fadeInUp animate__delay-1s"
          >Inovasi Pencarian Data Terbuka Pada Pemerintahan Provinsi Banten</h2>
          <h5
            v-show="device.mobile"
            class="text-center topik-title animate__animated animate__fadeInUp animate__delay-1s"
          >Inovasi Pencarian Data Terbuka Pada Pemerintahan Provinsi Banten</h5>
        </v-col>

      </v-row>
      <v-row class="mt-16 animate__animated animate__fadeInUp animate__delay-2s justify-around">

        <v-col :cols="device.desktop ?6:12">
          <v-row>
            <v-col
              :cols="device.desktop ? 4: 6"
              v-for="item in topics"
              :key="item.id"
            >
              <v-card
                flat
                class="pa-2 transparent"
                @click="openTopikDetail(item.id)"
              >
                <img
                  :src="item.icon"
                  alt=""
                  class="elevation-10 rounded-l topik-icon "
                >
                <v-card-text class="text-center">
                  {{ item.name }}
                </v-card-text>
              </v-card>
            </v-col>
          </v-row>
        </v-col>
        <v-col
          :cols="device.desktop ?6:12"
          v-show="device.desktop"
        >

          <v-row class="justify-center">
            <img
              src="/images/search-topik.jpeg"
              alt=""
              srcset=""
              width="50%"
              class="animate__animated animate__fadeInRight"
            >
            <span>
              <p style="text-align: justify;">
                Inovasi pencarian dalam upaya untuk meningkatkan efektivitas dan efisiensi dalam mencari informasi dari data yang ada. Inovasi ini dilakukan dengan menggunakan teknologi dan algoritma baru yang dapat membantu pengguna untuk menemukan informasi yang relevan dengan lebih cepat dan mudah.
              </p>
              <p style="text-align: justify;">
                Beberapa inovasi pencarian data yang terbaru termasuk penggunaan teknologi machine learning dan natural language processing untuk memahami konteks dari pertanyaan atau kata kunci yang dimasukkan oleh pengguna, dan kemudian menampilkan hasil pencarian yang lebih relevan dan terkait dengan pertanyaan atau kata kunci tersebut.
              </p>
            </span>
          </v-row>
        </v-col>

      </v-row>
    </v-container>
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";
export default {
  name: "modul-topik",
  data: () => ({
    topics: [],
  }),
  computed: {
    ...mapState(["device", "theme", "http"]),
  },
  mounted() {
    this.setPage({
      name: "topik",
      crud: false,
    });
    this.fetchTopics();
  },
  computed: {
    ...mapState(["device", "theme", "info", "snackbar", "loading", "http"]),
  },
  methods: {
    ...mapActions(["setPage", "getAppInfo", "snackbarClose"]),
    fetchTopics: async function () {
      try {
        let { data } = await this.http.get("daftar-topik");
        this.topics = data;
      } catch (error) {}
    },
    openTopikDetail: function (val) {
      this.$router.push({
        name: "topik-detail",
        params: {
          topic_uuid: val,
        },
      });
    },
  },
};
</script>

<style>
.topik-title {
  color: rgb(19, 12, 241);
}
.topik-icon {
  height: 100%;
  width: 100%;
}
</style>