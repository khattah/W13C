
<script setup lang="ts">
import { ref } from 'vue'

const songs = [
  {
    title: 'Sunrise',
    artist: 'The Morning Lights',
    song_id: 1,
    image_url: 'https://placehold.co/150?text=Sunrise'
  },
  {
    title: 'Ocean Breeze',
    artist: 'Blue Horizon',
    song_id: 2,
    image_url: 'https://placehold.co/150?text=Ocean'
  },
  {
    title: 'Night Drive',
    artist: 'City Lights',
    song_id: 3,
    image_url: 'https://placehold.co/150?text=Night'
  }
]

type Song = (typeof songs)[number]

const selectedSong = ref<Song | null>(null)

function selectSong(song: Song) {
  selectedSong.value = song
}
</script>

<template>
  <main class="playlist">
    <h1>My Music Playlist</h1>

    <h2>Song List</h2>

    <button
      v-for="song in songs"
      :key="song.song_id"
      class="song"
      @click="selectSong(song)"
    >
      <img :src="song.image_url" :alt="song.title" />
      <span>{{ song.title }} - {{ song.artist }}</span>
    </button>

    <h2>Playing Song</h2>

    <div v-if="selectedSong" class="playing">
      <img :src="selectedSong.image_url" :alt="selectedSong.title" />
      <h3>{{ selectedSong.title }}</h3>
      <p>{{ selectedSong.artist }}</p>
    </div>

    <p v-else>Please select a song from the playlist.</p>
  </main>
</template>

<style scoped>
.playlist {
  max-width: 600px;
  margin: 40px auto;
  padding: 25px;
  font-family: Arial, sans-serif;
  background: #f4f6f8;
  color: #222;
  border-radius: 12px;
}

.song {
  display: flex;
  align-items: center;
  gap: 15px;
  width: 100%;
  padding: 12px;
  margin-bottom: 10px;
  background: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  text-align: left;
}

.song:hover {
  background: #dceeff;
}

.song img {
  width: 65px;
  height: 65px;
  border-radius: 6px;
}

.playing {
  text-align: center;
  background: white;
  padding: 20px;
  border-radius: 10px;
}

.playing img {
  width: 150px;
  border-radius: 10px;
}
</style>
