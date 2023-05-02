<template>
  <div>
    <a class="welcome-link" href=".">
      <h1>Welcome to Spotify Search!</h1>
    </a>

    <h2 class="search-text">
      Search for your favourite music a bunch of different ways!
    </h2>

    <search-bar
      :token="bearerToken"
      @search-result="setSearchResult"
      @error-event="setError"
    >
    </search-bar>

    <!-- Idealy implement dynamic components (:is="component") here but it's proving tricky -->
    <error-message
      v-if="error"
      :error="error"
    ></error-message>

    <artist-info
      v-if="isArtistSearch"
      :artistInfo="searchResult"
    ></artist-info>

    <album-info
      v-if="isAlbumSearch"
      :albumInfo="searchResult"
    ></album-info>

    <playlist-info
      v-if="isPlaylistSearch"
      :playlistInfo="searchResult"
    ></playlist-info>

    <track-info
      v-if="isTrackSearch"
      :trackInfo="searchResult"
    ></track-info>

    <show-info
      v-if="isShowSearch"
      :showInfo="searchResult"
    ></show-info>

    <episode-info
      v-if="isEpisodeSearch"
      :episodeInfo="searchResult"
    ></episode-info>

    <audiobook-info
      v-if="isAudiobookSearch"
      :audiobookInfo="searchResult"
    ></audiobook-info>
  </div>
</template>

<script>
import SearchBar from './components/SearchBar.vue'
import ArtistInfo from './components/ResultsDisplays/ArtistInfo.vue'
import AlbumInfo from './components/ResultsDisplays/AlbumInfo.vue'
import PlaylistInfo from './components/ResultsDisplays/PlaylistInfo.vue'
import TrackInfo from './components/ResultsDisplays/TrackInfo.vue'
import ShowInfo from './components/ResultsDisplays/ShowInfo.vue'
import EpisodeInfo from './components/ResultsDisplays/EpisodeInfo.vue'
import AudiobookInfo from './components/ResultsDisplays/AudiobookInfo.vue'
import ErrorMessage from './components/ErrorMessage.vue'

export default {
  data() {
    return {
      selectedResultsComponent: 'albums',
      bearerToken: null,
      searchResult: null,
      error: null,
      clientId: 'f061dc9c17064d9a978a5ad029e8214d',
      clientSecret: 'a0e52f918364458f839acda63dbf9bb6'
    }
  },

  components: {
    SearchBar,
    ArtistInfo,
    AlbumInfo,
    PlaylistInfo,
    TrackInfo,
    ShowInfo,
    EpisodeInfo,
    AudiobookInfo,
    ErrorMessage
  },

  computed: {
    isArtistSearch() {
      return this.selectedResultsComponent === 'artists'
    },
    isAlbumSearch() {
      return this.selectedResultsComponent === 'albums'
    },
    isPlaylistSearch() {
      return this.selectedResultsComponent === 'playlists'
    },
    isTrackSearch() {
      return this.selectedResultsComponent === 'tracks'
    },
    isShowSearch() {
      return this.selectedResultsComponent === 'shows'
    },
    isEpisodeSearch() {
      return this.selectedResultsComponent === 'episodes'
    },
    isAudiobookSearch() {
      return this.selectedResultsComponent === 'audiobooks'
    }
  },

  methods: {
    getBearerToken() {
      fetch('https://accounts.spotify.com/api/token', {
        method: 'POST',
        headers: {
          'Content-Type':
            'application/x-www-form-urlencoded'
        },
        body: `grant_type=client_credentials&client_id=${this.clientId}&client_secret=${this.clientSecret}`
      })
        .then((response) => {
          if (response.ok) {
            return response.json()
          } else {
            throw new Error(
              'Something went wrong, please try again. If the problem persists, please shout angrily at the sky until I fix it, thank you.'
            )
          }
        })
        .then((data) => {
          this.bearerToken = data.access_token
        })
        .catch((error) => {
          {
            this.error = error
          }
        })
    },
    setError(error) {
      this.error = error
    },
    setSearchResult(data, searchType) {
      this.searchResult = data
      this.selectedResultsComponent = searchType
    }
    // Attempt at adding auth for any user. Not yet fully completed.

    // authorizeUser() {
    //   var client_id = this.clientId
    //   var redirect_uri = 'http://localhost:5173/'

    //   var app = express()

    //   app.get('/login', function (req, res) {
    //     var state = this.makeAuthId(16)
    //     var scope = 'user-read-private user-read-email'

    //     res.redirect(
    //       'https://accounts.spotify.com/authorize?' +
    //         querystring.stringify({
    //           response_type: 'code',
    //           client_id: client_id,
    //           scope: scope,
    //           redirect_uri: redirect_uri,
    //           state: state,
    //           show_dialog: true,
    //         })
    //     )
    //   })
    // },
    // makeAuthId(length) {
    //   let result = ''
    //   const characters =
    //     'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789'
    //   const charactersLength = characters.length
    //   let counter = 0
    //   while (counter < length) {
    //     result += characters.charAt(
    //       Math.floor(Math.random() * charactersLength)
    //     )
    //     counter += 1
    //   }
    //   return result
    // },
  },

  mounted() {
    // this.authorizeUser()
    this.getBearerToken()
  }
}
</script>
