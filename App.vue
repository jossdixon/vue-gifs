<template>
    <view>
        <!-- <header /> -->
        <scroll-view class="scroll-view" >
            <div v-if="!loading">
              <gif-item v-for="gif in gifs" :gif="gif" :key="gif.id" />
            </div>
            <view class="loading-container" :style="{flex: 1, justifyContent: 'center'}" v-if="loading">
              <activity-indicator size="large" color="#0000ff"></activity-indicator>
            </view>
        </scroll-view>
    </view>
</template>

<script>
  import Giphy from 'giphy-js-sdk-core';
  const client = Giphy('iVaof9h1KMnkGcZ1sv8AgKbB1u9GAfwz');
  import GifItem from './components/GifItem.vue';
  // import Header from './components/Header.vue';

  export default {
    name: 'App',
    data() {
      return {
        gifs: [],
        loading: true,
      };
    },
    async created() {
      const response = await client.trending('gifs', {limit: 20});
      this.gifs = response.data;
      this.loading = false;
    },
    components: { GifItem }
  };
</script>

<style>
    .scroll-view {
        padding-top: 20px;
        padding-bottom: 30px;
    }
    .loading-container {
        height: 600px;
    }
</style>
