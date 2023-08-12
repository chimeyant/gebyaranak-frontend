<template>
  <div>
    <videografis-component />
  </div>
</template>
  
<script>
import { mapState, mapActions } from "vuex";
import VideografisComponent from "./components/videografis/Index.vue";

export default {
  name: "videografis",
  components: {
    VideografisComponent,
  },
  mounted() {
    this.setPage({
      name: "videografis",
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