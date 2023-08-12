<template>
  <div>
    <integrasi-component />
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";
import IntegrasiComponent from "./components/integrasi/Index.vue";

export default {
  name: "integrasi",
  components: {
    IntegrasiComponent,
  },
  mounted() {
    this.setPage({
      name: "intgerasi",
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