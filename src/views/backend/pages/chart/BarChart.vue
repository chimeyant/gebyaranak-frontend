<script>
import { Bar } from "vue-chartjs";
import { mapActions, mapState } from "vuex";

export default {
  name: "bar-chart",
  extends: Bar,

  data: () => ({
    color: "#3F51B5",
  }),
  props: {
    title: String,
    labels: [],
    datas: [],
  },

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
            "JANUARI",
            "PEBRUARI",
            "MARET",
            "APRIL",
            "MEI",
            "JUNI",
            "JULI",
            "SEPTEMBER",
            "OKTOBER",
            "NOPEMBER",
            "DESEMBER",
          ], //this.labels,
          datasets: [
            {
              label: this.title,
              backgroundColor: "#608580",
              data: [10, 20, 30, 25, 5],
            },
          ],
        },
        {
          responsive: true,
          maintainAspectRatio: false,
          scales: {
            yAxes: [
              {
                ticks: {
                  beginAtZero: true,
                },
              },
            ],
          },
        }
      );
    },
  },
};
</script>
