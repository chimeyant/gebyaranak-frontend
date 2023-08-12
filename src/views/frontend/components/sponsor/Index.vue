<template>
  <div>
    <div class="text-center pt-10 title">DUKUNGAN</div>
    <div class="text-center body-1">
      Simpul Jaringan Inovasi Provinsi Banten
    </div>
    <div class="mt-10 mb-10">
      <v-container>
        <div class="sponsors-list-wrapper">
          <Carousel
            class="sponsor-list"
            :perPage="4"
          >
            <Slide
              v-for="(sponsor,index) in datas"
              :key="index"
            >
              <div class="sponsor-item">
                <img
                  :src="sponsor.image"
                  alt=""
                  style="width:75px ;"
                >
              </div>
            </Slide>
          </carousel>
        </div>
      </v-container>
    </div>
  </div>
</template>
  
<script>
import { mapState, mapActions } from "vuex";
import { Carousel, Slide } from "vue-carousel";
export default {
  name: "sponsor",
  components: {
    Carousel,
    Slide,
  },
  data: () => ({
    datas: [],
  }),
  computed: {
    ...mapState([
      "page",
      "device",
      "info",
      "snackbar",
      "device",
      "http",
      "loading",
      "theme",
    ]),
  },
  mounted() {
    this.fetchSponsors();
  },
  methods: {
    fetchSponsors: async function () {
      await this.http.get("sponsors").then((response) => {
        response.data.forEach((element) => {
          if (element.logo) {
            const row = {};
            row["id"] = element.id;
            row["name"] = element.name;
            row["image"] = element.logo;
            this.datas.push(row);
          }
        });
        //
      });
    },
  },
};
</script>

<style>
/* ==========================================================
! 08. SECTION: Sponsors
========================================================== */
.sponsor-item {
  height: 100px;
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  border-radius: 5px;
  background: #ffffff;
  line-height: 100px;
  text-align: center;
  margin-right: 10px;
}
.sponsor-item img {
  filter: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg'><filter id='grayscale'><feColorMatrix type='matrix' values='0.3333 0.3333 0.3333 0 0 0.3333 0.3333 0.3333 0 0 0.3333 0.3333 0.3333 0 0 0 0 0 1 0'/></filter></svg>#grayscale");
  /* Firefox 10+, Firefox on Android */
  filter: gray;
  /* IE6-9 */
  opacity: 0.7;
  -webkit-transition: all 0.4s ease-in-out;
  -moz-transition: all 0.4s ease-in-out;
  transition: all 0.4s ease-in-out;
}
.sponsor-item:hover img {
  filter: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg'><filter id='grayscale'><feColorMatrix type='matrix' values='1 0 0 0 0, 0 1 0 0 0, 0 0 1 0 0, 0 0 0 1 0'/></filter></svg>#grayscale");
  opacity: 1;
}
.sponsors-list-wrapper {
  width: 100%;
  overflow: hidden;
}
.sponsors-list {
  padding-top: 20px;
}
</style>