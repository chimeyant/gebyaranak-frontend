<template>
  <div
    class="hero-content"
    style="background-image: url('images/satudata_b.png');"
  >
    <v-container>
      <v-row>
        <v-col :cols="device.desktop ? 4: 12">
          <div :class="device.desktop ? `mt-5 banner-title animate__animated animate__lightSpeedInRight`:`mt-5 ml-5 display-1 blue--text animate__animated animate__lightSpeedInRight`">
            Banten Opendata
          </div>
          <div :class="device.desktop ? `banner-subtitle animate__animated animate__fadeInUp animate__delay-1s`:`banner-subtitle animate__animated animate__fadeInUp animate__delay-1s ml-5` ">
            Di sini Anda bisa akses koleksi data dan artikel terlengkap di Banten dengan cepat, mudah, dan akurat dibantu berbagai fitur bermanfaat.
          </div>
          <div :class="device.desktop ? `mt-10 animate__animated animate__fadeInUp animate__delay-2s`:`mt-10 animate__animated animate__fadeInUp animate__delay-2s mr-5 ml-5` ">
            <v-text-field
              outlined
              class=""
              placeholder="Pencarian Data"
              color="orange darken-1"
              prepend-inner-icon="search"
            ></v-text-field>
          </div>
        </v-col>
        <v-col
          v-show="device.desktop"
          cols="8"
        >
          <div class="video-warp">
            <div class="video-figure">
              <div class="inner-figure">
                <div class="overlay" />
                <div class="video">
                  <youtube
                    :video-id="videoId"
                    :player-vars="playerVars"
                    :width="1080"
                    :height="720"
                    ref="youtube"
                    @playing="playing"
                    @ended="ended"
                  />
                </div>
              </div>
            </div>
          </div>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<style lang="scss" scoped>
@import "./banner-style.scss";
</style>

<script>
import { mapState } from "vuex";
import youtube from "vue-youtube";

export default {
  components: {},
  data() {
    return {
      videoId: "jlRJXYdPtQU",
      playerVars: {
        autoplay: 1,
        controls: 0,
        rel: 0,
        showinfo: 0,
        mute: 1,
        origin: "http://localhost:8001",
      },
      yt: youtube,
      play: false,
      playCtrl: true,
      //cover: imgAPI.agency[0],
    };
  },
  methods: {
    playing() {
      this.play = true;
      this.playCtrl = true;
    },
    ended() {
      this.player.playVideo();
    },
    togglePause() {
      this.playCtrl = !this.playCtrl;
      if (this.playCtrl) {
        this.player.playVideo();
      } else {
        this.player.pauseVideo();
      }
    },
  },
  computed: {
    ...mapState(["device"]),
    player() {
      return this.$refs.youtube.player;
    },
  },
};
</script>

<style>
.hero-content {
  background-size: cover;
  height: 500px;
}
</style>
