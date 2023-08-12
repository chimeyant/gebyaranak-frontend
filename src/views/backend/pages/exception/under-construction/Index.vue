<template>
  <div>
    <v-container>
      <v-col cols="12">
        <v-row class="justify-center">

          <img
            src="/images/under-contruction.png"
            alt=""
            srcset=""
            style="width: 100wH;"
          >
        </v-row>
      </v-col>
    </v-container>
  </div>
</template>
  
  <script>
import { mapState, mapActions } from "vuex";

export default {
  name: "under-contruction",
  data: () => ({}),
  computed: {
    ...mapState(["page", "device", "theme"]),
  },
  mounted() {
    this.setPage({
      crud: true,
      dataUrl: "#",
      pagination: false,
      title: "INFORMATION",
      subtitle: "Under Contruction",
      edit: false,
      breadcrumbs: [
        {
          text: "PAGE",
          disabled: true,
          href: "",
        },
        {
          text: "Under Contruction",
          disabled: true,
          href: "",
        },
      ],
      actions: {
        refresh: true,
        add: true,
        edit: true,
        delete: true,
        bulkdelete: false,
        export: false,
        print: false,
        help: false,
      },
    });
  },
  methods: {
    ...mapActions(["setPage"]),
  },
};
</script>