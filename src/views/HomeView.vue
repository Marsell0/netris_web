<template>
  <div class="_container">
    <div class="main">
      <div class="main__video">
        <VideoPlayer></VideoPlayer>
      </div>
      <div class="main__sub">
        <div class="sub__count">
          count
        </div>
        <div class="sub__graph">
          graph
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import LineGraph from '@/components/LineGraph.vue'
import DragUpload from '@/components/DragUpload.vue';
import VideoPlayer from '@/components/VideoPlayer.vue'

export default{
  components:{
    LineGraph, DragUpload, VideoPlayer
  },
  data: () => {
    return {
      videoOptions: {
        autoplay: true,
        controls: true,
        sources: [
          {
            src:
              '/path/to/video.mp4',
              type: 'video/mp4'
          }
        ]
      }
    }
  }
}

</script>

<style scoped>
._container {
  max-width: 1533px;
  max-height: 4320px;
  margin: 0px auto;
  display: flex;
}
.main {
  background-color: rgb(110, 109, 109);
  display: flex;
  flex-direction: row;
  flex: 1;
  padding: 1%;
}
.main__video {
  background-color: aqua;
  flex: 1;
  width: 100%;
  height: 56.25%;
}
.main__sub {
  background-color: green;
  flex: 0.5;
}
.sub__count {
  background-color: blue;
}
.sub__graph {
  background-color: yellow;
}
</style>
