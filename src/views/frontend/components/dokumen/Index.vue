<template>
  <div class="mt-10">
    <v-container>
      <v-row>
        <h3 class="display-1 font-weight-bold">Dokumen</h3>
      </v-row>
      <v-row class="mt-10 text-body-2">
        Temukan kumpulan data-data mentah berupa tabel yang bisa diolah lebih lanjut di sini. Open Data Banten menyediakan akses ke beragam koleksi dokumen dari seluruh Organisasi Perangkat Daerah di Provinsi Banten.
      </v-row>
      <v-row class="mt-10">
        <v-col cols="12">
          <v-text-field
            outlined
            placeholder="Pencarian dataset"
            append-icon="search"
            color="orange"
          ></v-text-field>
        </v-col>
        <v-col cols="12">
          <v-row class="pl-3 pr-3 pt-5">
            <span class="text-body-2 font-weight-medium">
              {{ datas.meta.total }} Dokumen
            </span>
            <v-spacer>
            </v-spacer>
            <v-select
              label="Urutkan"
              outlined
              dense
              style="max-width: 300px;"
            ></v-select>
          </v-row>
        </v-col>
        <v-divider></v-divider>
        <v-col cols=12>
          <div>
            <v-divider></v-divider>
            <v-list three-line>
              <template v-for="(item, index) in datas.data">
                <v-subheader
                  v-if="item.header"
                  :key="item.header"
                  v-text="item.header"
                ></v-subheader>

                <v-divider
                  v-else-if="item.divider"
                  :key="index"
                  :inset="item.inset"
                ></v-divider>

                <v-list-item
                  v-else
                  :key="item.title"
                >

                  <img
                    :src="item.icon"
                    alt=""
                    srcset=""
                    width="100"
                    class="mr-2 mb-2"
                  >

                  <v-list-item-content class="mr-5">
                    <v-row>
                      <v-col cols="10">
                        <div class="text-body-1">
                          {{ item.title }}
                        </div>
                      </v-col>
                      <v-col
                        cols="2"
                        class="text-center pt-10"
                      >
                        <v-btn
                          outlined
                          small
                          color="green darken-2"
                          @click="postDownload(item.id)"
                        >
                          <v-icon
                            class="mr-1"
                            small
                          > mdi-cloud-download</v-icon> Download
                        </v-btn>
                      </v-col>
                    </v-row>
                    <div>
                      <v-row class="pl-3 text-body-2">
                        <v-icon
                          class="mr-2"
                          small
                        >mdi-office-building-outline</v-icon><span class="mr-2">{{ item.opd }}</span>
                        <v-icon
                          class="mr-2"
                          small
                        >mdi-map</v-icon><span class="mr-2">Provinsi Banten</span>
                      </v-row>
                      <v-row class="mt-5 pl-3 text-body-2">
                        <v-icon
                          class="mr-2"
                          small
                        >mdi-calendar</v-icon><span class="mr-2">2022-2023</span>
                        <v-icon
                          class="mr-2"
                          small
                        >mdi-book</v-icon><span class="mr-2">{{ item.topik }}</span>
                        <v-icon
                          class="mr-2"
                          small
                        >mdi-clock-check</v-icon><span class="mr-2">2 Hari yang lalu</span>
                      </v-row>
                    </div>
                    <div></div>
                  </v-list-item-content>
                  <v-list-item-action>
                    <div>
                      <v-icon
                        small
                        class="mr-2 green--text"
                      >mdi-cloud-download</v-icon><span class="text-body-2">{{ item.counter }}</span>
                    </div>
                  </v-list-item-action>
                </v-list-item>
              </template>
            </v-list>
            <v-row class="justify-end mt-10">
              <div class="mt-4 mb-5">
                <v-select
                  label="Per Halaman"
                  outlined
                  dense
                ></v-select>
              </div>
              <v-spacer></v-spacer>
              <div class="mt-4 mb-5">
                <v-pagination
                  color="green"
                  v-model="page"
                  :length="datas.meta.last_page"
                ></v-pagination>
              </div>
            </v-row>
          </div>
        </v-col>
      </v-row>
      </v-row>
    </v-container>
  </div>
</template>
  
<script>
import { mapState, mapActions } from "vuex";
export default {
  name: "modul-dokumen",
  data: () => ({
    page: 1,
    datas: [],
  }),
  computed: {
    ...mapState(["device", "theme", "http"]),
  },
  mounted() {
    this.setPage({
      name: "document",
      crud: false,
    });
    this.fetchDocuments();
  },
  computed: {
    ...mapState(["device", "theme", "info", "snackbar", "loading", "http"]),
  },
  methods: {
    ...mapActions(["setPage", "getAppInfo", "snackbarClose", "setLoading"]),
    fetchDocuments: async function () {
      try {
        let { data } = await this.http.get("daftar-dokumen");
        this.datas = data;
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
    postDownload: async function (val) {
      try {
        this.setLoading({ dialog: true, text: "Sedang proses download" });
        let {
          data: { code, success, message, url, errors },
        } = await this.http.get("dokumen-download/" + val);
        window.open(url, "__blank");
      } catch (error) {
        console.log(error);
      } finally {
        this.setLoading({ dialog: false, text: "" });
      }
    },
  },
};
</script>