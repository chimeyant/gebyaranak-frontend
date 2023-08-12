<script>
import { Bar } from "vue-chartjs";
import { mapActions, mapState } from "vuex";

export default {
  name: "permohonan-bulan",
  extends: Bar,

  data: () => ({
    color: "#3F51B5",
  }),

  computed: {
    ...mapState(["http", "theme"]),
  },

  mounted() {
    this.fetchData();
    //this.color = this.theme.color;
  },
  methods: {
    fetchData: async function () {
      //let { data } = await this.http.get(
      "api/supervisor/dashboard-pengajuan-per-bulan";
      //);
      this.renderChart(
        {
          labels: [
            "KAB. TANGERANG",
            "KAB. SERANG",
            "KAB. PANDEGLANG",
            "KAB. LEBAK",
            "KOTA. SERANG",
            "KOTA. CILEGON",
            "KOTA. TANGERANG",
            "KOTA. TANGERANG SELATAN",
          ],
          datasets: [
            {
              label: "Grafik Inflasi Provinsi Banten",
              backgroundColor: "#3F51B5",
              data: [2, 2, 4.5, 3, 2, 3, 4, 2, 1],
            },
          ],
        },
        { responsive: true, maintainAspectRatio: false }
      );
    },
  },
};
</script>
