<template>
  <v-app class="back">
    <v-container>
      <v-carousel
              cycle
              show-arrows-on-hover
              :height="1000"
      >
        <v-carousel-item
                v-for="(item,i) in items"
                :key="i"
                :src="item.src"
                reverse-transition="fade-transition"
                transition="fade-transition"
        ></v-carousel-item>
      </v-carousel>
    </v-container>
  </v-app>
</template>
<script>
  export default {
    name: 'HelloWorld',

    data: () => ({
      colors: [
        'indigo',
        'warning',
        'pink darken-2',
        'red lighten-1',
        'deep-purple accent-4',
      ],
      items: [
        {
          src: require('../assets/img/markdown/clone.png')
        },
        {
          src: require('../assets/img/markdown/dl-zippng.png')
        },
        {
          src: require('../assets/img/markdown/cmd.png')
        },
        {
          src: require('../assets/img/markdown/vuejs.jpg')
        },
        {
          src: require('../assets/img/markdown/matrix.jpg')
        }
      ],
      ecosystem: [
        {
          text: 'vuetify-loader',
          href: 'https://github.com/vuetifyjs/vuetify-loader',
        },
        {
          text: 'github',
          href: 'https://github.com/vuetifyjs/vuetify',
        },
        {
          text: 'awesome-vuetify',
          href: 'https://github.com/vuetifyjs/awesome-vuetify',
        },
      ],
      importantLinks: [
        {
          text: 'Documentation',
          href: 'https://vuetifyjs.com',
        },
        {
          text: 'Chat',
          href: 'https://community.vuetifyjs.com',
        },
        {
          text: 'Made with Vuetify',
          href: 'https://madewithvuejs.com/vuetify',
        },
        {
          text: 'Twitter',
          href: 'https://twitter.com/vuetifyjs',
        },
        {
          text: 'Articles',
          href: 'https://medium.com/vuetify',
        },
      ],
      whatsNext: [
        {
          text: 'Explore components',
          href: 'https://vuetifyjs.com/components/api-explorer',
        },
        {
          text: 'Select a layout',
          href: 'https://vuetifyjs.com/layout/pre-defined',
        },
        {
          text: 'Frequently Asked Questions',
          href: 'https://vuetifyjs.com/getting-started/frequently-asked-questions',
        },
      ],
    }),
  };
</script>

<style scoped>
  .back{
    background: #2C5364;
  }
</style>
