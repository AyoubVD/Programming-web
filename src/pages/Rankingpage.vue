
<template>
  <div>
    <!-- Button -->
    <button class="cybr-btn" @click="goToPage('home')">
      Go home
    </button>
    <!-- FlexBox div  -->
    <div class="center">
      <!-- H1  -->
      <h1>Ranking for</h1>
      <!-- Table -->
      <table>
        <tr>
          <!-- Table headers -->
          <th class="hoofd">Ranking for</th>
          <th class="hoofd">Play song</th>
          <th class="hoofd">Title</th>
          <th class="hoofd">Artist</th>
          <th class="hoofd">Points</th>
        </tr>
        <!-- Items themselves -->
        <!-- For every song in the fetched JSON -->
        <tr v-for="(song, i) in songs" :key="i">
          <td>#{{ i + 1 }}</td>
          <td><iframe :src="song.spotify" width="100%" height="80" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe></td>
          <td>{{ song.title }}</td>
          <td>{{ song.artist }}</td>
          <td>{{ song.totalPoints }}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "Rankingpage",
  data() {
    return {
      //Initialze songs array
      songs: [],
    };
  },
  methods: {
    goToPage(page) {
      this.$emit("change-page", page);
    },
    fetchSongs() {
      const url = "http://webservies.be/eurosong/Songs";

      fetch(url)
        .then((response) => {
          //JSON parse the output
          return response.json();
        })
        .then((songs) => {
          //Call both methods to get all votes and artists that are needed to be displayed
          this.fetchVO(songs);
          this.fetchArtists(songs);
        });
    },

    fetchArtists(songs) {
      //Fetch artists from Elke's artists endpoint
      const url = "http://webservies.be/eurosong/Artists";
      fetch(url)
        .then((response) => {
          //JSON parse output
          return response.json();
        })
        .then((artists) => {
          //Map each song and get the specified artist from the nested objects
          songs.map((song) => {
            const a = artists.find((artist) => artist.id == song.artist);
            song.artist = a.name;
            return song;
          });
          this.songs = songs;
        });
    },
    fetchVO(songs) {
      //Fetch artists from Elke's votes endpoint
      const url = "http://webservies.be/eurosong/Votes";

      fetch(url)
        .then((response) => {
          //JSON parse the output
          return response.json();
        })
        .then((votes) => {
          let allPoints = 0;
          //Loop over songs
          songs.map((song) => {
            song.totalPoints = 0;
            votes
              .filter((vote) => vote.songID == song.id)
              .forEach((element) => {
                if (element.songID == song.id) {
                  song.totalPoints += element.points;
                  allPoints += element.points;
                }
              });
            return song;
          });

            let fullTotal = 0;
            songs.forEach((song) => {
              song.percentage = Number(
                ((song.totalPoints / allPoints) * 100).toFixed(2)
              );
              fullTotal += song.totalPoints
            });

          this.songs = songs.sort((y, z) => z.totalPoints - y.totalPoints);
        });
    },
  },
  mounted() {
    this.fetchSongs();
  },
};
</script>