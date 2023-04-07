<template>
    <div class="max-w-3xl px-4 mx-auto sm:px-6 xl:max-w-5xl xl:px-0">
      <div class="pt-6 pb-8 space-y-2 md:space-y-5">
        <h1
          class="troikaFont text-3xl font-extrabold leading-9 tracking-tight text-gray-900 dark:text-gray-100 sm:text-4xl sm:leading-10 md:text-6xl md:leading-14"
        >
          My Friends SMP
        </h1>
        <p class="text-lg leading-7 text-gray-500 dark:text-gray-400">
          The streamers I watch the most and also friends of mine.
        </p>
      </div>
      <main class="relative mb-auto">
        <div class="">
          <div class="container py-12">
            <div class="flex flex-wrap -m-4">
                <streamer-card v-for="(streamer, streamerIndex) in streamersData" :key="streamerIndex" :streamer="streamer" class="py-1 px-2"/>
            </div>
          </div>
        </div>
      </main>
    </div>
  </template>
  
  <script>
import StreamerCard from '../../components/StreamerCard.vue';
  import streamersData from "../../data/streamers.js";
  export default {
    data() {
      return {
    
        streamersData: streamersData,
      };
    },
    head: {
      title: "Elfini7y | Streamers",
      meta: [
        { charset: "utf-8" },
        { name: "viewport", content: "width=device-width, initial-scale=1" },
        {
          hid: "description",
          name: "description",
          content: "The best streamers on Twitch",
        },
      ],
      link: [{ rel: "icon", type: "image/x-icon", href: "/favicon.ico" }],
    },
  };
  </script>
  