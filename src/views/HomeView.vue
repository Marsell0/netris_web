<template>
  <div class="_container">
    <div class="main">
      <div class="main__video">
        <VideoPlayer></VideoPlayer>
      </div>
      <div class="main__sub">
        <div class="sub__count">
          <ul class="count__list">
            <li class="list__item" v-for="item in items" :key="item.message"> {{ item.message }}: {{ item.count }}</li>
          </ul>
        </div>
        <div class="sub__button">
          <DragUpload @drop.prevent="drop" @change="selectedFile"></DragUpload>
          <span class="file-info">Файл: {{ dropzoneFile.name }}</span>
        </div>
      </div>
    </div>
    <div class="graph">
      <LineGraph></LineGraph>
    </div>
  </div>
</template>

<script>
import LineGraph from '@/components/LineGraph.vue'
import DragUpload from '@/components/DragUpload.vue';
import VideoPlayer from '@/components/VideoPlayer.vue'
import { ref } from 'vue';

export default{
  components:{
    LineGraph, DragUpload, VideoPlayer
  },
  setup() {
    let items = [
        {message: 'Трактор', count: '0'},
        {message: 'Грузовая машина', count: '1'},
        {message: 'Кран', count: '0'},
        {message: 'Экскаватор', count: '2'},
    ];
    let dropzoneFile = ref('0');
    const drop = (e) => {
        dropzoneFile.value = e.dataTransfer.files[0];
    }
    const selectedFile = () => {
      dropzoneFile.value = document.querySelector('.dropzone__input').files[0];
    }
    return {items, drop, dropzoneFile, selectedFile};
  }
}

</script>

<style scoped>
._container {
  max-width: 1533px;
  max-height: 4320px;
  margin: 0px auto;
  display: flex;
  flex-direction: column;
}
.main {
  background-color: rgb(199, 198, 198);
  border-radius: 25px;
  display: flex;
  flex-direction: row;
  flex: 1;
  padding: 1%;
  margin-top: 4%;
}
.main__video {
  flex: 1;
  width: 100%;
  height: 56.25%;
}
.main__sub {
  display: flex;
  flex: 0.5;
  flex-direction: column;
}
.sub__count {
  background-color: rgb(233, 233, 233);
  margin: 0 0 1% 1%;
  border-top-right-radius: 10px;
}
.sub__button {
  font-size: 25px;
  margin: auto;
  display: flex;
  flex-direction: column;
  flex: 1 1 auto;
  
}
.count__list{
  list-style-type: none;
  text-align: start;
  margin-top: 0px;
  padding: 10% 0 10% 3%;
}
.list__item{
  font-size: 25px;
  color: black;
}

@media screen and (max-width: 900px) {
  .list__item{
    font-size: 15px;
    color: black;
  }
}
</style>
