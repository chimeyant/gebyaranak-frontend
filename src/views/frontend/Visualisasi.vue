<template>
  <div>
    <visualisasi-component />
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";
import VisualisasiComponent from "./components/visualisasi/Index.vue";

export default {
  name: "visualisasi",
  components: {
    VisualisasiComponent,
  },
  mounted() {
    this.setPage({
      name: "visualisasi",
    });
  },
  computed: {
    ...mapState(["page", "theme", "device"]),
  },
  methods: {
    ...mapActions(["setPage"]),
  },
};
</script>