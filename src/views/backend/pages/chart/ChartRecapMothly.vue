<script>
import { Bar } from "vue-chartjs";
import { mapActions, mapState } from "vuex";

export default {
  name: "bar-chart-recap-mothly",
  extends: Bar,

  data: () => ({
    color: "#3F51B5",
    colors: [],
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
      let { data } = await this.http.get("api/v2/dashboard/recap-monthly");

      data.forEach((element) => {
        this.color = this.getDynamiColor();
        this.colors.push(this.color);
      });

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
            "AGUSTUS",
            "SEPTEMBER",
            "OKTOBER",
            "NOPEMBER",
            "DESEMBER",
          ], //this.labels,
          datasets: [
            {
              label: this.title,
              backgroundColor: this.colors,
              data: data,
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
    getDynamiColor: function () {
      var r = Math.floor(Math.random() * 255);
      var g = Math.floor(Math.random() * 255);
      var b = Math.floor(Math.random() * 255);
      return "rgb(" + r + "," + g + "," + b + "," + 0.5 + ")";
    },
  },
};
</script>
