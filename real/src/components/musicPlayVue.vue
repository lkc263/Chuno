<template>
  <div>
    <div>
      <img
        class="music"
        :v-if="audio.isPlaying"
        @click="audio.isPlaying ? pause(audio) : play(audio)"
        v-bind:src="`${audio.isPlaying ? soundOn : soundOff}`"
      />
    </div>
  </div>
</template>

<script>
import bgm from "@/assets/audio/bgm.mp3";
import soundOn from "@/assets/sound_on.png";
import soundOff from "@/assets/sound_off.png";

export default {
  props: {
    isPlay: Boolean,
    start: Boolean,
  },

  data() {
    return {
      bgm,
      soundOn,
      soundOff,
      audio: {
        id: "music-opening",
        name: "MusicOpening",
        file: new Audio(bgm),
        isPlaying: false,
      },
    };
  },

  mounted() {
    this.audio.file.addEventListener("ended", () => {
      this.audio.file.play();
      this.audio.file.currentTime = 0;
      this.audio.isPlaying = true;
    });
  },

  updated() {
    if (!this.isPlay) {
      this.pause(this.audio);
      this.audio.file.currentTime = 0;
    }
    if (this.start) {
      this.play(this.audio);
      this.$emit("offStart");
    }
  },

  methods: {
    play(audio) {
      audio.isPlaying = true;
      audio.file.play();
    },

    pause(audio) {
      audio.isPlaying = false;
      audio.file.pause();
    },
  },
};
</script>

<style>
.music {
  position: absolute;
  width: 40px;
  height: 40px;
  cursor: pointer;
}
</style>
