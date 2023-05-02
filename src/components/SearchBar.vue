<template>
  <div >
    <input
      type="text"
      placeholder="Find your muse..."
      v-model="searchTerm"
      @keydown.enter="
        anySearch(searchTerm, selectedSearchType)
      "
    />
    <select v-model="selectedSearchType">
      <option
        v-for="searchType in searchTypeStrings"
        :value="searchType.query"
      >
        {{ searchType.ui }}
      </option>
    </select>
    <button
      class="zoom"
      type="button"
      @click="anySearch(searchTerm, selectedSearchType)"
    >
      Search
    </button>
    <div>
      <p>Results per search</p>
      <select
        v-model="pageLimit"
      >
        <option>5</option>
        <option>15</option>
        <option>25</option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchTerm: '',
      searchTypeStrings: [
        { query: 'artist', ui: 'Artist' },
        { query: 'album', ui: 'Album' },
        { query: 'playlist', ui: 'Playlist' },
        { query: 'track', ui: 'Track' },
        { query: 'show', ui: 'Show' },
        { query: 'episode', ui: 'Episode' },
        { query: 'audiobook', ui: 'Audiobook' }
      ],

      selectedSearchType: 'artist',
      pageLimit: 5
    }
  },

  props: ['token'],

  emits: ['search-result', 'error-event'],

  methods: {
    anySearch(query, searchType) {
      if (this.searchTerm === '') {
        this.emitError(
          '"Please enter a search term. Though I would love to, I cannot pull music from the air!"'
        )
        return
      }
      this.emitError(null)
      fetch(
        `https://api.spotify.com/v1/search?q=${query}&type=${searchType}&limit=${this.pageLimit}`,
        {
          headers: {
            Authorization: `Bearer ${this.token}`
          }
        }
      )
        .then((response) => {
          if (response.ok) {
            return response.json()
          }
        })
        .then((data) => {
          const typeString = this.selectedSearchType + 's'
          if (
            data[typeString].items.length < 1 ||
            data[typeString].items[0] === null
          ) {
            this.emitError(
              'Nothing found for that search, sorry!'
            )
            return
          }
          this.$emit(
            'search-result',
            data[typeString].items,
            typeString
          )
        })
        .catch((error) => {
          console.log(error)
          this.emitError(
            'Something went wrong, please try again. If the problem persists, please shout angrily at the sky until I fix it, thank you.'
          )
        })
    },
    emitError(error) {
      this.$emit('error-event', error)
    }
  }
}
</script>

<style scoped>
input {
  vertical-align: top;
  width: auto;
  height: 100%;
  border-radius: 8px;
  border: 1px solid transparent;
  font-size: xx-large;
  margin-right: 1rem;
  background-color: #e1e1e1;
}

input:focus,
input:hover,
textarea {
  box-shadow: 0 0 20px #719ece;
}

select {
  vertical-align: top;
  height: 41px;
  width: auto;
  border: 1px solid transparent;
  border-radius: 8px;
  background-color: #e1e1e1;
  font-size: large;
}

select:hover {
  box-shadow: 0 0 20px #719ece;
}

button {
  vertical-align: top;
  width: auto;
  height: 41px;
  margin-left: 1rem;
  border-radius: 8px;
  color: #e1e1e1;
  border: 1px solid #e1e1e1;
  background-color: #000000;
  cursor: pointer;
  font-size: large;
}

button:hover {
  box-shadow: 0 0 20px #719ece;
}

.zoom {
  transition: transform 0.2s;
}
.zoom:hover {
  transform: scale(1.1);
}
</style>
