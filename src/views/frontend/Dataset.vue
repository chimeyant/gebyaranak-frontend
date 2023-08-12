<template>
  <div>
    <dataset-component />
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";
import DatasetComponent from "./components/Dataset/Index.vue";

export default {
  name: "dataset",
  components: {
    DatasetComponent,
  },
  mounted() {
    this.setPage({
      name: "dataset",
      crud: false,
    });
  },
  computed: {
    ...mapState(["device", "theme", "info", "snackbar", "loading"]),
  },
  methods: {
    ...mapActions(["setPage", "getAppInfo", "snackbarClose"]),
  },
};
</script>