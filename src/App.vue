<template>
  <v-app dark>
    <v-content>
      <v-container>
        <!-- The player components go here -->
        <title-bar></title-bar>
        <playlist-panel 
          @selecttrackhihi="selectTrack" 
          :selectedTrack="selectedTrack"  
          :playlist="playlist"
        >
        </playlist-panel>
      </v-container>
    </v-content>
  </v-app>
</template>
 
<script>
  import TitleBar from './components/TitleBar.vue' // IMPORT the component
  import PlaylistPanel from './components/PlaylistPanel.vue' // IMPORT the component
  import { Howl } from 'howler'

  export default {
    components: {
      TitleBar,
      PlaylistPanel
    },
    data () {
      return {
        playlist: [
          {title: "Lake louise", artist: "Various Artist", howl: null, display: true},
          {title: "Ngay ngo", artist: "Various Artist", howl: null, display: true}
        ],
        selectedTrack: null 
      }
    },
    created: function () {
      this.playlist.forEach((track) => {
        let file = track.title.replace(/\s/g, "_")
        track.howl = new Howl({
          src: [`./playlist/${file}.mp3`]
        })
      })
    },
    methods: {
      selectTrack (track) {
        this.selectedTrack = track
      }
    }
  }
</script>