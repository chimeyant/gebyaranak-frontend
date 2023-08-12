<template>

  <div class="page-not-found">
    <img
      src="/images/404.jpeg"
      alt=""
      srcset=""
      style="width: 100wH;"
    >

  </div>

</template>
  
<script lang="js">
import { mapActions, mapState } from "vuex";

export default {
  name: "Login",
  components: {
  },
  computed: {
    ...mapState([
      "snackbar",
      "theme",
      "thememode",
      "dialog",
      "user",
      "menus",
      "page",
      "form",
      "device",
      "loading",
      "upload",
      "info",
      "http",
      "table",
      "records",
    ]),
  },
  data: () => ({}),
  mounted() {
    this.getAppInfo().then(() => {
      window.document.title = this.info.app_name;
    });
  },
  methods: {
    ...mapActions(["getAppInfo",])
  },
};
</script>
  
<style>
.page-not-found {
  margin: 0;
  position: absolute;
  padding: 10px;
  top: 25%;
  transform: translateY(-50%);
  transform: translateX(50%);
}
</style>