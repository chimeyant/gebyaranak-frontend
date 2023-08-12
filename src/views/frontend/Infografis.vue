<template>
  <div>
    <infografis-component />
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";
import InfografisComponent from "./components/infografis/Index.vue";

export default {
  name: "infografis",
  components: {
    InfografisComponent,
  },
  mounted() {
    this.setPage({
      name: "infografis",
      crud: false,
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