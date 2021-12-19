<template>
  <q-page>
    <div style="height: 100vh; padding-top: -50px" class="column">
      <div class="col-1"></div>
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
                <q-img :src="whip.icon"></q-img>
              </template>
              <template v-else>
                <q-spinner-bars size="md" />
              </template>
              {{ whip.name }}
            </q-btn>
          </div>
        </div>
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
        icon: "/icons/1.png",
        src: "/audio/1.mp3",
        showing: true,
      },
      whips: [
        {
          name: "Whip 1",
          icon: "/icons/1.png",
          src: "/audio/1.mp3",
          showing: true,
        },
        {
          name: "Whip 2",
          icon: "/icons/2.png",
          src: "/audio/2.mp3",
          showing: true,
        },
        {
          name: "Whip 3",
          icon: "/icons/3.png",
          src: "/audio/3.mp3",
          showing: true,
        },
        {
          name: "Whip 4",
          icon: "/icons/4.png",
          src: "/audio/4.mp3",
          showing: true,
        },
        {
          name: "Whip 5",
          icon: "/icons/5.png",
          src: "/audio/5.mp3",
          showing: true,
        },
        {
          name: "Whip 6",
          icon: "/icons/6.png",
          src: "/audio/6.mp3",
          showing: true,
        },
        {
          name: "Whip 7",
          icon: "/icons/7.png",
          src: "/audio/7.mp3",
          showing: true,
        },
        {
          name: "Whip 8",
          icon: "/icons/8.png",
          src: "/audio/8.mp3",
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
      var audio = new Audio(whip.src);
      audio.volume = this.volume;
      audio.play();
      audio.addEventListener("playing", () => {
        whip.showing = false;
      });
      audio.addEventListener("ended", () => {
        whip.showing = true;
      });
    },
  },
});
</script>
