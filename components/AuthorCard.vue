<template>
  <div class="md:fixed">
    <div class="md:block flex justify-center items-center">
      <div
        :class="`shadow-xl md:h-60 md:w-60 h-40 w-40 rounded-full overflow-hidden relative ${!firstTimeHover ? 'border-4 border-indigo-900 animate-pulse' : ''}`"
        @mouseover="showRandomGif"
        @mouseleave="hideRandomGif"
      >
        <div class="absolute top-0 lef-0 h-full w-full flex items-center justify-center bg-indigo-700 bg-opacity-40" v-if="!firstTimeHover">
          <div class="ml-2 text-white font-medium troikaFont border-b-4 border-gray-900">Hover on me</div>
        </div>
        <nuxt-img
          v-if="!mouseOver"
          :src="mouseOver ? randomGif : siteMetadata.author_image"
          loading="lazy"
          alt="me"
          class="h-full w-full object-cover"
        />
        <img :src="randomGif" v-else class="h-full w-full object-cover"/>
      </div>
      <div class="mb-2 mx-7 mt-4 justify-center items-center">
        <h1
          class="md:text-3xl text-2xl text-gray-800 font-bold dark:text-blue-100 troikaFont"
        >
          {{ siteMetadata.author }}
        </h1>
        <div class="md:text-lg text-gray-600 dark:text-blue-100">
          {{ siteMetadata.position }}
        </div>
        <a
          :href="`mailto:${siteMetadata.email}`"
          class="text-gray-600 md:hidden mt-1 dark:text-blue-100"
        >
          {{ siteMetadata.email }}
        </a>
      </div>
    </div>

    <div class="mx-7 hidden md:block">
      <div class="my-2 text-gray-600 flex dark:text-blue-100">
        <Mail class="mr-2"/>
        <a :href="`mailto:${siteMetadata.email}`"> {{ siteMetadata.email }}</a>
      </div>
      <div class="my-2 text-gray-600 flex dark:text-blue-100">
        <Glob class="mr-2"/>
        <p>{{ siteMetadata.location }}</p>
      </div>
      <div class="my-2 text-gray-600 flex dark:text-blue-200">
        <Github class="mr-2"/>
        <a :href="siteMetadata.github" target="_blank"> {{ siteMetadata.githubUser }}</a>
      </div>
      <div class="my-2 text-gray-600 flex dark:text-blue-200">
        <Twitch class="mr-2"/>
        <a :href="siteMetadata.twitch" target="_blank"> {{ siteMetadata.twitch_user }}</a>
      </div>
    </div>
  </div>
</template>

<script>
import Mail from "../assets/icon/mail.svg?inline";
import Glob from "../assets/icon/glob.svg?inline";
import Github from "../assets/icon/github_new.svg?inline";
import Twitch from "../assets/icon/twitch.svg?inline";
import siteMetaInfo from "@/data/sitemetainfo";
export default {
  components: { Mail, Glob, Github, Twitch },
  data: () => {
    return {
      firstTimeHover: false,
      mouseOver: false,
      siteMetadata: siteMetaInfo,
      randomGif: "",
    };
  },
  methods:{
    async showRandomGif(){
      if(this.mouseOver) return;
      const response = await fetch(`https://api.giphy.com/v1/gifs/random?api_key=${process.env.GiphyApiKey}`)
      if(response.status == 200){
        const data = await response.json();
        this.randomGif = data.data.images.original.webp;
        console.log(this.randomGif)
      }
      this.mouseOver = true;
      this.firstTimeHover = true;
    },
    hideRandomGif(){
      console.log("hideRandomGif");
      this.mouseOver = false;
    }
  }
};
</script>
<style scoped>
@keyframes pulse {
  0% {
    border-width: 4px !important;
    opacity: 1;
  }
  50% {
    border-width: 8px !important;
    opacity: 0.95;
  }
  100% {
    border-width: 4px !important;
    opacity: 1;
  }
}
</style>