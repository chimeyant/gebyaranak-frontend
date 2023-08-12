<template>
  <v-app-bar
    app
    light
    color="transparent"
    absolute
    style="height: 85px;"
    elevation="0"
  >
    <v-toolbar-title>
      <div class="pl-5 pr-5">
        <img
          src="/images/logo.png"
          width="160px"
          height="40px"
          alt="logo"
          :class="device.desktop ? `animate__animated animate__tada ant-header-logo`:`ant-header-logo-mobile`"
          @click="$router.push({name:'home'})"
        >
      </div>

    </v-toolbar-title>
    <v-spacer />
    <v-list
      color="transparent"
      class="d-flex white light  mt-4  mb-5"
      style="margin-right: 150px !important;"
    >
      <template v-for="(menu,index) in menus">
        <v-list-item
          active-class="green darken-1 white--text rounded-pill animate__animated animate__bounce "
          class="hidden-sm-and-down rounded-pill"
          link
          :to="menu.route"
          v-if="menu.type=='item'"
        >
          <v-list-item-title class="font-weight-bold">{{ menu.title }}</v-list-item-title>
        </v-list-item>

        <v-menu
          offset-y
          v-if="menu.type=='subMenu'"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              active-class="green darken-1 white--text rounded-pill"
              class="font-weight-bold rounded-pill "
              v-bind="attrs"
              v-on="on"
              text
              style="text-transform: unset !important;height: 50px;"
            >
              {{ menu.title }}
            </v-btn>
          </template>
          <v-list>
            <v-list-item
              v-for="(item, index) in menu.submenus"
              :key="index"
              :to="item.route"
            >
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item>
          </v-list>
        </v-menu>

      </template>
    </v-list>

    <v-menu
      offset-y
      width="300"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          v-show="device.mobile"
          icon
          light
          v-bind="attrs"
          v-on="on"
          class="mt-4"
        >
          <v-icon color="black">mdi-menu</v-icon>
        </v-btn>
      </template>
      <v-card width="200">
        <v-list>
          <v-list-item>
            <v-list-item-title @click="$router.push({ name: 'home' })">
              Beranda
            </v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-title @click="$router.push({name:'infografis'})">
              Data Inovasi
            </v-list-item-title>
          </v-list-item>
          <v-list-item>
            <v-list-item-title @click="$router.push({ name: 'dataset' })">
              Kompetisi
            </v-list-item-title>
          </v-list-item>
          <v-list-item>
            <v-list-item-title @click="$router.push({ name: 'produsen-data' })">
              Klinik Inovasi
            </v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-title @click="$router.push({ name: 'dokumen' })">
              Faq
            </v-list-item-title>
          </v-list-item>
          <v-list-item>
            <v-list-item-title @click="$router.push({ name: 'login' })">
              Login
            </v-list-item-title>
          </v-list-item>

        </v-list>
      </v-card>
    </v-menu>
  </v-app-bar>
</template>

<script>
import { mapState, mapActions } from "vuex";
export default {
  name: "HeaderComponent",

  data: () => ({
    menus: [
      { title: "Beranda", route: "/home", type: "item" },
      {
        title: "Data Inovasi",
        route: "#",
        type: "subMenu",
        submenus: [
          {
            title: "Seluruh Inovasi",
            icon: "mdi-clover",
            route: "/repository",
            type: "item",
          },
          {
            title: "Grafik Inovasi",
            icon: "mdi-clover",
            route: "#",
            type: "item",
          },
          {
            title: "Peta Inovasi",
            icon: "mdi-clover",
            route: "#",
            type: "item",
          },
        ],
      },
      {
        title: "Kompetisi",
        route: "/kompetisi",
        type: "subMenu",
        submenus: [
          {
            title: "IGA",
            icon: "mdi-clover",
            route: "#",
            type: "item",
          },
          {
            title: "SINOVIC",
            icon: "mdi-clover",
            route: "#",
            type: "item",
          },
        ],
      },
      {
        title: "Klinik Inovasi",
        route: "/klinik-inovasi",
        type: "subMenu",
        submenus: [
          {
            title: "Tim Kajian",
            icon: "mdi-clover",
            route: "#",
            type: "item",
          },
          {
            title: "Inovator",
            icon: "mdi-clover",
            route: "#",
            type: "item",
          },
        ],
      },
      { title: "FAQ", route: "/faq", type: "item" },
      { title: "Login", route: "/login", type: "item" },
    ],
  }),
  mounted() {},
  computed: {
    ...mapState(["device", "theme", "info", "page"]),
  },
};
</script>

<style>
.v-toolbar__title {
  display: flex;
  font-size: 20px;
  font-weight: 600;
  color: cornflowerblue;
}

::before {
  border-radius: 30px;
}

span.hidden-sm-and-down.header-title {
  font-size: 20px;
  color: grey;
}

.ant-header-title {
  font-family: people;
}
.ant-header-subtitle {
  font-size: 13px;
  font-family: sans-serif;
}
.ant-header-logo {
  margin-top: 15px;
  margin-left: 150px;
}
.ant-header-logo-mobile {
  margin-left: 2px;
}
</style>