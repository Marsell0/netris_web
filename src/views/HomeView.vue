<template>
  <div class="_container">
    <div class="main">
      <div class="main__video">
        <img class="main__video" :src="videoF"/>
      </div>
      <div class="main__sub">
        <div class="sub__count">
          <ul class="count__list">
            <li class="list__item" v-for="item in items" :key="item.message"> {{ item.message }}: {{ item.count }}</li>
          </ul>
        </div>
        <div class="sub__button">
          <DragUpload @drop.prevent="drop" @change="selectedFile"></DragUpload>
        </div>
      </div>
    </div>
    <div class="graph">
      <LineGraph></LineGraph>
    </div>
  </div>
  <p  class="sueta" style="{display: hidden;}">h</p>
</template>

<script>
import LineGraph from '@/components/LineGraph.vue'
import DragUpload from '@/components/DragUpload.vue';
import VideoPlayer from '@/components/VideoPlayer.vue'
import { ref } from 'vue';
import axios from 'axios';

export default{
  updated(){
    console.log('updated')
  },
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
    let filename = ref('')
    let fileActive = ref(false)
    let path = ref('http://127.0.0.1:5000/video_feed?filename=')
    let res = ref('')
    let videoActive = ref(false)
    let videoF = localStorage.getItem('video')

    const drop = (e) => {
        dropzoneFile.value = e.dataTransfer.files[0];
    }
    const selectedFile = (event) => {
      dropzoneFile.value = document.querySelector('.dropzone__input').files[0];
      filename.value = document.querySelector('.sueta').textContent
      console.log('selectedFile ' + document.querySelector('.sueta').textContent)
      console.log('res ' + res)
      videoActive.value = true
      localStorage.setItem('video', path.value + localStorage.getItem('name'))
    } 
    return {items, drop, dropzoneFile, selectedFile, filename, fileActive,path,videoF};
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
  background-color: #27293D;
  border-radius: 5px;
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
  background-color: #27293D;
  margin: 0 0 1% 1%;
  border-top-right-radius: 10px;
}
.sub__button {
  font-size: 25px;
  margin: auto;
  display: flex;
  flex-direction: column;
  flex: 1 1 auto;
  margin-left: 5px;
  margin-right: 0;
}
.count__list{
  list-style-type: none;
  text-align: start;
  margin-top: 0px;
  padding: 10% 0 10% 3%;
  border: solid #3A9B6C;
  border-top-right-radius: 10px;

}
.list__item{
  font-size: 25px;
  color: #F1FFE0;
}
.file-info{
  display: flex;
  color: #F1FFE0;
}
@media screen and (max-width: 900px) {
  .list__item{
    font-size: 15px;
    color: black;
  }
}
</style>
