<template>
  <v-app id="inspire">
    <v-navigation-drawer
            v-model="drawer"
            :clipped="$vuetify.breakpoint.lgAndUp"
            app
    >
      <v-list dense>
        <template v-for="item in items">
          <v-row
                  v-if="item.heading"
                  :key="item.heading"
                  align="center"
          >
            <v-col cols="6">
              <v-subheader v-if="item.heading">
                {{ item.heading }}
              </v-subheader>
            </v-col>
            <v-col
                    cols="6"
                    class="text-center"
            >
              <a
                      href="#!"
                      class="body-2 black--text"
              >EDIT</a>
            </v-col>
          </v-row>
          <v-list-group
                  v-else-if="item.children"
                  :key="item.text"
                  v-model="item.model"
                  :prepend-icon="item.model ? item.icon : item['icon-alt']"
                  append-icon=""
          >
            <template v-slot:activator>
              <v-list-item-content>
                <v-list-item-title>
                  {{ item.text }}
                </v-list-item-title>
              </v-list-item-content>
            </template>
            <v-list-item
                    v-for="(child, i) in item.children"
                    :key="i"
                    link
                    :to="child.link"
            >
              <v-list-item-action v-if="child.icon">
                <v-icon>{{ child.icon }}</v-icon>
              </v-list-item-action>
              <v-list-item-content>
                <v-list-item-title>
                  {{ child.text }}
                </v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list-group>
          <v-list-item
                  v-else
                  :key="item.text"
                  link
          >
            <v-list-item-action>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title >
                {{ item.text }}
              </v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </template>
      </v-list>
    </v-navigation-drawer>

    <Navbar @toggleDrawer="toggle" :title="title"></Navbar>
    <v-main>
      <v-container>
      <router-view />
      </v-container>
    </v-main>


  </v-app>
</template>

<script>
  import Navbar from "./Navbar";
  export default {
    components: {
      Navbar
    },
    props: {
      source: String,
    },
    data: () => ({
      title: 'Library App',
      dialog: false,
      drawer: null,
      items: [

        {
          icon: 'mdi-chevron-up',
          'icon-alt': 'mdi-chevron-down',
          text: 'Books',
          model: true,
          children: [
            { icon: 'mdi-menu', text: 'List Books', link: 'books' },
            { icon: 'mdi-plus', text: 'Add Book', link: 'bookForm'},
            { icon: 'mdi-plus', text: 'Add Category', link: 'category' },
          ],
        },
        {
          icon: 'mdi-chevron-up',
          'icon-alt': 'mdi-chevron-down',
          text: 'More',
          model: false,
          children: [
            { text: 'Import' },
            { text: 'Export' },
            { text: 'Print' },
            { text: 'Undo changes' },
            { text: 'Other contacts' },
          ],
        },
        { icon: 'mdi-history', text: 'History' , link: '/history'},
        { icon: 'mdi-cog', text: 'Settings' },
        { icon: 'mdi-message', text: 'Send E-mail' },
        { icon: 'mdi-help-circle', text: 'Help' },
        { icon: 'mdi-cellphone-link', text: 'App downloads' },
        { icon: 'mdi-logout', text: 'Logout' },
      ],
    }),
    methods: {
      toggle(v) {
        console.log(v)
        this.drawer = v;
      }
    }
  }
</script>