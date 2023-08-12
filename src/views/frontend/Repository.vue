<template>
  <div>
    <repository />
  </div>
</template>
  
  <script>
import { mapState, mapActions } from "vuex";
import Repository from "./components/repository/Index.vue";

export default {
  name: "home",
  components: {
    Repository,
  },
  data: () => ({}),
  mounted() {
    this.setPage({
      name: "home",
      crud: false,
    });
  },
  computed: {
    ...mapState(["device", "theme", "info", "snackbar", "loading", "page"]),
  },
  methods: {
    ...mapActions(["setPage", "getAppInfo", "snackbarClose"]),
  },
};
</script>
  
  
  
  
  