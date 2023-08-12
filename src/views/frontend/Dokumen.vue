<template>
  <div>
    <dokumen-component />
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";
import DokumenComponent from "./components/dokumen/Index.vue";

export default {
  name: "dokumen",
  components: {
    DokumenComponent,
  },
  mounted() {
    this.setPage({
      name: "dokumen",
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