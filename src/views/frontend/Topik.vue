<template>
  <div>
    <topik-component />
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";
import TopikComponent from "./components/Topik/Index.vue";

export default {
  name: "topik",
  components: {
    TopikComponent,
  },
  mounted() {
    this.setPage({
      name: "topik",
      crud: false,
    });
  },
  computed: {
    ...mapState(["device", "theme", "info", "snackbar", "loading", "http"]),
  },
  methods: {
    ...mapActions(["setPage", "getAppInfo", "snackbarClose"]),
  },
};
</script>