<script>
import { Pie } from "vue-chartjs";
import { mapActions, mapState } from "vuex";

export default {
  extends: Pie,
  data: () => ({
    jmll: 0,
    jmlp: 0,
    data: [],
    gradient: null,
    colors: [],
  }),
  props: {
    title: String,
    labels: [],
    datas: [],
  },
  computed: {
    ...mapState(["http"]),
  },
  created() {
    //this.fetchdata();
  },
  mounted() {
    this.fetchdata();
    this.gradient = this.$refs.canvas
      .getContext("2d")
      .createLinearGradient(0, 0, 0, 450);
    this.gradient2 = this.$refs.canvas
      .getContext("2d")
      .createLinearGradient(0, 0, 0, 450);

    this.gradient.addColorStop(0, "rgba(255, 0,0, 0.5)");
    this.gradient.addColorStop(0.5, "rgba(255, 0, 0, 0.25)");

    this.gradient2.addColorStop(0, "rgba(0, 231, 255, 0.9)");
    this.gradient2.addColorStop(0.5, "rgba(0, 231, 255, 0.25)");
  },
  methods: {
    fetchdata: async function () {
      this.datas.forEach((element) => {
        const color = this.getDynamiColor();
        this.colors.push(color);
      });

      try {
        this.renderChart(
          {
            labels: this.labels,
            datasets: [
              {
                backgroundColor: ["red", "orange"],
                data: this.datas,
              },
            ],
          },
          {
            responsive: true,
            maintainAspectRatio: false,
            legend: {
              position: "bottom",
            },
          }
        );
      } catch (error) {}
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