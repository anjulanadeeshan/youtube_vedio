<template>
  <div style=" overflow-y: scroll">
    <div style="">
      <TitleComponent title="Youtube Data Api" sub_title="Just search whatever You want"/>

      <v-container class="fill-height" >
        <v-responsive class="align-center text-center">

          <v-text-field
            clearable
            label="What would you like to watch today?"
            prepend-icon="mdi mdi-video-4k-box"
            variant="solo-inverted"
            v-model="search_query"
          ></v-text-field>

          <v-btn
            prepend-icon="mdi-vuetify"
            append-icon="mdi-vuetify"
            variant="tonal"
            @click="callYoutubeDataApi"
          >
            Let's Go
          </v-btn>
          <!--RESALT-->
          <v-container>
            <v-row no-gutters>
              <v-col
                v-for="video in search_result"
                :key="video"
                cols="12"
                sm="4"
              >
                <v-sheet class="ma-2 pa-2">
                  <PreviewCard :title="video.snippet.title"
                               :chanel="video.snippet.channelTitle"
                               :image="video.snippet.thumbnails.high.url" @click="playVideo(video.id.videoId)"
                               @triggerparent="playVideo">

                  </PreviewCard>
                </v-sheet>
              </v-col>
            </v-row>
          </v-container>

        </v-responsive>
      </v-container>
      <v-row justify="center">
        <v-dialog
          v-model="dialog"
          fullscreen
          :scrim="false"
          transition="dialog-bottom-transition">

          <v-card>
            <v-toolbar
              dark
              color="primary"
            >
              <v-btn
                icon
                dark
                @click="dialog = false"
              >
                <v-icon>mdi-close</v-icon>
              </v-btn>
            </v-toolbar>
            <div ref="player"></div>
          </v-card>
        </v-dialog>
      </v-row>
    </div>

  </div>
</template>

<script>

// AIzaSyBqo1HahjH89PeJOINB_pembjoObLDnzhw - apikey
// AIzaSyAMuvkxn3s3j7QvD0BI5I06tSA2_1RXNdE
import PreviewCard from "@/components/PreviewCard.vue";
import axios from "axios";
import YouTubePlayer from "youtube-player";
import TitleComponent from "@/components/Title.vue";

const apiKey = 'AIzaSyBqo1HahjH89PeJOINB_pembjoObLDnzhw';
const apiUrl = 'https://www.googleapis.com/youtube/v3/search';
export default
{
  components: {TitleComponent, PreviewCard},

  data() {
    return {
      search_query: null,
      search_result: [],
      dialog: false,
      player:null,
      wrapper:null
    };
  },
  methods: {
    async callYoutubeDataApi() {
      const keyword = this.search_query;
      const response = await axios.get(apiUrl, {
          params: {
              key:apiKey, part:'snippet', type: 'video', q:keyword, maxResults: 12}
      });
      this.search_result = response.data.items;
    },
    playVideo(videoId) {
      this.dialog = true;
      setTimeout(()=>{
        this.wrapper = this.$refs.player;
        this.player = YouTubePlayer(this.wrapper, {
          videoId: videoId,
          width: '100%',
          height:'100%',
          playerVars: {
            autoplay: true
          }
       },2000);
      });
    }
  }
}
</script>

<style>
</style>

