<template>
  <q-page>
    <div style="height: 100vh" class="column">
      <div class="col-1 q-pt-lg">
        <div class="row justify-center">
          <div class="col-8">
            <q-list dense>
              <q-item>
                <q-item-section avatar>
                  <q-icon color="teal" name="volume_up" />
                </q-item-section>
                <q-item-section>
                  <q-slider
                    v-model="volume"
                    :min="0"
                    :max="1"
                    :step="0.1"
                    label
                    color="teal"
                  />
                </q-item-section>
              </q-item>
            </q-list>
          </div>
        </div>
      </div>
      <div class="col-2">
        <div class="text-center">
          <q-img
            alt="Whip Sound App"
            src="~assets/banana-emoji.gif"
            loading="lazy"
            width="100px"
            height="100px"
          />
        </div>
      </div>
      <div class="col-2">
        <div class="text-center">
          <q-btn stack color="primary" @click="playRandomSound" class="q-pa-lg">
            <template v-if="!randomWhip">
              <q-icon name="shuffle" size="lg"></q-icon>
            </template>
            <template v-else>
              <q-spinner-bars size="md" />
            </template>
            <div class="text-capitalize">Random Whip</div>
          </q-btn>
        </div>
      </div>
      <div class="col-1"></div>
      <div class="col-6">
        <div class="row q-px-xl">
          <div
            class="col-3 text-center q-mb-xl"
            v-for="whip in whips"
            :key="whip.name"
          >
            <q-btn
              stack
              color="primary"
              @click="playSound(whip)"
              class="q-pa-lg"
            >
              <template v-if="whip.showing">
                <q-img :src="getImgUrl(whip.number)"></q-img>
              </template>
              <template v-else>
                <q-spinner-bars size="md" />
              </template>
              {{ whip.name }}
            </q-btn>
          </div>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "PageIndex",
  data() {
    return {
      volume: 1,
      randomWhip: null,
      defaultWhip: {
        name: "Whip 1",
        icon: "statics/1.png",
        src: "/audio/1.mp3",
        showing: true,
      },
      whips: [
        {
          name: "Whip 1",
          number: "1",
          showing: true,
        },
        {
          name: "Whip 2",
          number: "2",
          showing: true,
        },
        {
          name: "Whip 3",
          number: "3",
          showing: true,
        },
        {
          name: "Whip 4",
          number: "4",
          showing: true,
        },
        {
          name: "Whip 5",
          number: "5",
          showing: true,
        },
        {
          name: "Whip 6",
          number: "6",
          showing: true,
        },
        {
          name: "Whip 7",
          number: "7",
          showing: true,
        },
        {
          name: "Whip 8",
          number: "8",
          showing: true,
        },
      ],
    };
  },
  methods: {
    playRandomSound() {
      this.playSound(this.whips[Math.floor(Math.random() * (6 - 1) + 1)]);
    },
    playSound(whip) {
      var audio = new Audio(this.getAudioUrl(whip.number));
      audio.volume = this.volume;
      audio.play();
      audio.addEventListener("playing", () => {
        whip.showing = false;
      });
      audio.addEventListener("ended", () => {
        whip.showing = true;
      });
    },
    getImgUrl(pic) {
      return new URL(`../assets/icons/${pic}.png`, import.meta.url).href      
    },
    getAudioUrl(file) {
      return new URL(`../assets/audio/${file}.mp3`, import.meta.url).href      
    },
  },
});
</script>
