<template>
  <div>
    <button @click="goToPage('home')">Go to home</button>
    <h1>Ranking</h1>
    <div v-for="song in songs" :key="song.id">
      {{ song.title }} - {{ song.artist.name }} - NaN hier komt som van punten NaN
      <!-- <div v-for="vote in votes" :key="vote.id">
        <div v-if="vote.songID == song.id">
          {{ vote.points }}
        </div>
      </div> -->
    </div>
  </div>
</template>

<script>
export default {
  name: "Rankingpage",

  data() {
    return {
      songs: [],
      votes: [],
    };
  },
  computed: {
    total: function(){
      return this.items.reduce(function(prev, item){
   return sum + item.price; 
     },);
    },
  },


  mounted() {
    this.fetchSongs();
    this.fetchArtists();

    this.fetchVO();
  },

  methods: {
    goToPage(page) {
      this.$emit("change-page", page);
    },

    // data methods
    fetchSongs() {
      // Get all songs
      const url = "http://webservies.be/eurosong/Songs";

      fetch(url)
        .then((response) => {
          return response.json();
        })
        .then((response) => (this.songs = response))
        .then((votes) => {
          this.fetchArtists(votes);
        });
    },

    fetchVO() {
      // Get all songs
      const url = "http://webservies.be/eurosong/Votes";

      fetch(url)
        .then((response) => {
          return response.json();
        })
        .then((response) => (this.votes = response));
    },

    fetchArtists(songs) {
      // Get all artist
      const url = "http://webservies.be/eurosong/Artists";

      fetch(url)
        .then((response) => {
          // response is text, so convert to json
          return response.json();
        })
        .then((artists) => {
          // loop over array songs with forEach method
          songs.map((song) => {
            // find the artist in an array
            const artist = artists.find((artist) => artist.id == song.artist);

            // replace the id by the artist object
            song.artist = artist;

            // return the new object
            return song;
          });

          // change data of songs, so everything will get rerenderd;
          this.songs = songs;
        });
    },

    fetchVotes(songs) {
      // Get all artist
      const url = "http://webservies.be/eurosong/Votes";

      fetch(url)
        .then((response) => {
          // response is text, so convert to json
          return response.json();
        })
        .then((votes) => {
          // loop over array songs with forEach method
          songs.map((song) => {
            // find the artist in an array
            const vote = votes.find((vote) => vote.songID == song.id);
          
          
            // replace the id by the artist object
            song.id = vote;

            // return the new object
            return song;
          }),
          // loop over array songs with forEach method
          songs.map((song) => {
            const vote = votes.find((vote) => vote.songID == song.id);
              songs.map((song) => {
                const sum = votes.find((vote) => vote.songID == song.id);
              }),
          
            // replace the id by the artist object
            song.id = vote;

            // return the new object
            return song;
          })
          



          // change data of songs, so everything will get rerenderd;
          this.songs = songs;
        });
    },
  },
};
</script>