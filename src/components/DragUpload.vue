<template>
  <div @dragenter.prevent="toggleActive" 
        @dragleave.prevent="toggleActive" 
        @dragover.prevent 
        @drop.prevent="toggleActive" :class="{ 'active-dropzone': active}" class="dropzone">
    <span>Drag&Drop</span>
    <span>или</span>
    <label class="dropzone__label" for="dropzoneFiles">Выбрать файл</label>
    <input class="dropzone__input" name="video" type="file" id="dropzoneFiles" ref="file" v-on:change="handleFileUpload()" accept="video/*" />
  </div>
  <!-- <form action="/upload" method="post" enctype="multipart/form-data">
        <input type="file" name="video" accept="video/*">
        <input type="submit" value="Upload">
    </form> -->
</template>

<script setup>
import { ref, getCurrentInstance } from 'vue';
import axios from 'axios';

    const active = ref(false)
    let path = ref('http://127.0.0.1:5000/')
    let path_up = ref('http://127.0.0.1:5000/video_feed?filename=')
    let file = ref('')
    let formData = new FormData();
    let res = ref('')
    let f = ref('')
    
    let instance = getCurrentInstance()
    // instance.refs.file.value = null

    const uploadFile = async () =>{
      console.log('start')
      res = await axios.post(`${path.value}/upload`, formData, {
                  headers: {
                    'Content-Type': 'multipart/form-data',
                    'Access-Control-Allow-Origin' : '*',
                    'Access-Control-Allow-Methods':'GET,PUT,POST,DELETE,PATCH,OPTIONS',
                  }
                }
      )
      console.log('suc')
      console.log(res.data)
      f.value = res.data
      console.log(f.value)
      document.querySelector('.sueta').text = f.value
      console.log('sueta ' + document.querySelector('.sueta').text)
      let div = document.createElement('div')
      document.body.append(div)
      localStorage.setItem('name', f.value)
      console.log('проверка нейм' + localStorage.getItem('name'))
      localStorage.setItem('video', path_up.value + localStorage.getItem('name'))
      console.log('проверка видео' + localStorage.getItem('video'))
      location.reload()
    }

    const handleFileUpload = async () => {
      file.value = instance.refs.file.files[0]
      formData.append('video', file.value);
      console.log('handle ' + file.value)
      await uploadFile()
    }

    const toggleActive =  () => {
      active.value = !active.value; 
    }


</script>

<style scoped>
.dropzone{
  background-color: #27293D;
  color: black;
  display: flex;
  flex-direction: column;
  border: dashed #3A9B6C ;
  justify-content: center;
  align-items: center;
  border-bottom-right-radius: 15px;
  transition: 0.3s ease all;
  flex: 1 1 auto;
  color: #F1FFE0;
  margin-bottom: 5px;
}
.dropzone > span{
  margin-bottom: 10px;
}
.dropzone__label{
  color: #F1FFE0;
  background-color: #3A9B6C;
  transition: 0.3s ease all;
  padding: 8px 12px;
  margin: 0 5% 0 5%;
}
.dropzone__input{
  display: none;
}
.active-dropzone{
  color: #F1FFE0;
  border-color: #F1FFE0;
  background-color: #3A9B6C;
}
.active-dropzone > label{
  background-color: #F1FFE0;
  color: #3A9B6C;
}
</style>


<!-- <template>
  <n-upload
    action="https://www.mocky.io/v2/5e4bafc63100007100d8b70f"
  >
    Upload  
  </n-upload>
</template>

<script>
import { defineComponent } from 'vue'
import { NUpload } from 'naive-ui'

export default defineComponent({
  components: {
    NUpload,
  }
})
</script> -->