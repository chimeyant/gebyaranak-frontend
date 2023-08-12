<template>

  <section class="hightlight-section ">
    <v-parallax
      dark
      src="/images/innovation5.jpeg"
    >
      <v-container>

        <div>

          <div>
            <carousel-3d
              width="400"
              height="350"
              autoplay
              :controls-visible="true"
              :controls-prev-html="'&#10092; '"
              :controls-next-html="'&#10093;'"
              :controls-width="30"
              :controls-height="60"
              :clickable="true"
            >
              <slide
                v-for="(item,index) in highlights"
                :index="index"
                style="border-radius: 10px; background-color: white;"
              >
                <div class="pa-5">
                  <img
                    :src="item.url"
                    alt=""
                    srcset=""
                    class="highlight-slide-image"
                    width="100px"
                  >
                  <div class="highlight-slide-title black--text">
                    {{ "Judul Inovasi...!!" }}
                    <div>

                      <span class="mt-1 ml-2 black--text body-2 grey--text ">{{ "01/01/2022" }}</span>
                    </div>
                  </div>
                  <div class="pa-3 mt-5 mb-5">
                    <v-row>
                      <v-btn
                        @click=""
                        color="green"
                      >Selengkapnya</v-btn>

                    </v-row>
                  </div>
                </div>
              </slide>

            </carousel-3d>
          </div>
          <div class="black--text mt-10">
            <h2 class="text-center white--text">Inovasi Terbaru</h2>
          </div>
        </div>
      </v-container>
    </v-parallax>
  </section>

</template>
<script>
import { mapState, mapActions } from "vuex";
import { Carousel3d, Slide } from "vue-carousel-3d";

export default {
  name: "highlight-data",
  components: {
    Carousel3d,
    Slide,
  },
  data: () => ({
    highlights: [
      {
        url: "https://cdn.pixabay.com/photo/2017/10/04/09/56/laboratory-2815641_1280.jpg",
      },
      {
        url: "https://source.unsplash.com/user/c_v_r/1900x800",
      },
      {
        url: "https://source.unsplash.com/user/c_v_r/1600×900",
      },
      {
        url: "https://source.unsplash.com/user/c_v_r/1600×900",
      },
      {
        url: "https://source.unsplash.com/user/c_v_r/1600×900",
      },
    ],
  }),
  computed: {
    ...mapState(["page", "device", "http"]),
  },
  created() {
    this.setPage({
      crud: false,
    });
  },
  mounted() {
    this.fetchHighlights().then(() => {
      setTimeout(function () {
        window.dispatchEvent(new Event("resize"));
      }, 250);
    });
  },
  methods: {
    ...mapActions(["setPage"]),
    fetchHighlights: async function () {
      // let {
      //   data: { data },
      // } = await this.http.get("highlights");
      // this.highlights = data;
    },
    openTopic: function (val) {
      this.$router.push({
        name: "topik-detail",
        params: {
          topic_uuid: val,
        },
      });
    },
    openData: function (tablename, refuuid) {
      if (tablename == "dataset") {
        this.$router.push({
          name: "dataset-detail",
          params: {
            dataset_uuid: refuuid,
          },
        });
      }
      if (tablename == "visualisasi") {
        this.$router.push({
          name: "visualisasi-detail",
          params: {
            visualization_uuid: refuuid,
          },
        });
      }
      if (tablename == "infografik") {
        this.$router.push({
          name: "infografis-detail",
          params: {
            infographic_uuid: refuuid,
          },
        });
      }

      if (tablename == "videografis") {
        this.$router.push({
          name: "videografis",
        });
      }

      if (tablename == "document") {
        this.$router.push({
          name: "dokumen",
        });
      }
    },
  },
};
</script>

<style>
.hightlight-section {
  margin-top: 0px;
  background-color: rgb(160, 158, 158);
  background-size: 100%;
}
.highlight-title {
  font-size: 30px;
  font-weight: bold;
  color: rgb(9, 124, 51);
  letter-spacing: 3px;
  padding-bottom: 10px;
}
.highlight-slide-image {
  height: 200px;
  width: 100px;
  border: 1px solid rgb(96, 94, 94);
  border-radius: 5px;
}
.highlight-slide-title {
  font-size: 14pt;
  font-weight: bold;
}
</style>