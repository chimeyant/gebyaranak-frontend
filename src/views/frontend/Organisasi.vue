<template>
  <div>
    <organisasi-component />
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";
import OrganisasiComponent from "./components/organisasi/Index.vue";

export default {
  name: "organisasi",
  components: {
    OrganisasiComponent,
  },
  mounted() {
    this.setPage({
      name: "organisasi",
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