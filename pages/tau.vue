<template>
  <div>
    <v-layout row>
      <page-banner
        :logo="tauSymbol"
        :style="{ 'background-image': 'url(/tau.jpg)' }"
      />
    </v-layout>
    <v-layout row>
      <front-page-section-white 
        :sections="tauSections"
      />
    </v-layout>
    <v-layout row>
      <front-page-footer />
    </v-layout>
  </div>
</template>

<script>
import axios from 'axios'
import VueMarkdown from 'vue-markdown'
import PageBanner from '~/components/PageBanner.vue'
import FrontPageSectionWhite from '~/components/FrontpageSectionWhite.vue'
import GenericSection from '~/components/GenericSection.vue'
import FrontPageFooter from '~/components/FrontpageFooter.vue'

export default {
  components: {
    PageBanner,
    VueMarkdown,
    FrontPageSectionWhite,
    GenericSection,
    FrontPageFooter
  },
  head() {
    return {
      title: 'House Blivande – Studio Tau',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: `
          Blivande is a co-working space, 
          arts workshop, makerspace and 
          community center in Stockholm.`
        },
        {
          hid: 'keywords',
          name: 'keywords',
          content: `
          co-working, co-working space, makerspace, 
          arts workshop, community, burn, burning man, 
          participatory, co-creation, stockholm`
        },
        {
          hid: 'og:image',
          name: 'og:image',
          content: 'http://www.blivande.com/tau.jpg'
        }
      ]
    }
  },
  async asyncData({ params }) {
    let blivande_content = await axios.get(
      'https://participio-api.herokuapp.com/discourse/blivande/frontpage'
    )
    let pagebanner = 'taubanner'
    let tauSymbol = 'stsymbol.png'
    let tauAbout = blivande_content['data']['59']
    let tauJoin = blivande_content['data']['60']
    let betaMakers = blivande_content['data']['58']
    let betaPageContent = blivande_content['data']['57']
    let tauPageContent = blivande_content['data']['36']
    let joinBetaTitle = 'Join Beta'
    let tauSections = [
      {
        title: 'What is Studio Tau?',
        text: tauAbout,
        image: 'tau-square.jpg',
        id: 1
      },
      {
        title: 'How do I join?',
        text: tauJoin,
        image: 'tau-square-alt.jpg',
        link: 'https://forum.blivande.com/c/tau',
        button: 'Join the community',
        id: 2
      }
    ]

    return {
      pagebanner,
      tauSymbol,
      tauAbout,
      tauJoin,
      betaMakers,
      betaPageContent,
      tauPageContent,
      tauSections,
      joinBetaTitle
    }
  }
}
</script>

<style>
@import url('../static/css/font-awesome.min.css');
@import url('https://fonts.googleapis.com/css?family=IBM+Plex+Sans:200,200i,400,400i');
@import url('../static/css/typography.css');
@import url('../static/css/banner.css');
@import url('../static/css/row.css');
@import url('../static/css/box.css');
@import url('../static/css/button.css');
@import url('../static/css/form.css');
@import url('../static/css/icon.css');
@import url('../static/css/image.css');
@import url('../static/css/list.css');
@import url('../static/css/actions.css');
@import url('../static/css/icons.css');
@import url('../static/css/table.css');
@import url('../static/css/wrapper.css');
@import url('../static/css/spotlights.css');
@import url('../static/css/features.css');
@import url('../static/css/header.css');
@import url('../static/css/footer.css');
@import url('../static/css/nav-panel.css');
</style>
