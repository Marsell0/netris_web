<template>
  <div @dragenter.prevent="toggleActive" 
        @dragleave.prevent="toggleActive" 
        @dragover.prevent 
        @drop.prevent="toggleActive" :class="{ 'active-dropzone': active}" class="dropzone">
    <span>Drag&Drop</span>
    <span>или</span>
    <label class="dropzone__label" for="dropzoneFiles">Выбрать файл</label>
    <input class="dropzone__input" type="file" id="dropzoneFiles"  />
  </div>
</template>

<script>
import { ref } from 'vue';
// import axios from 'axios';

export default{
  setup() {
    const active = ref(false)

    // let file = ''
    // let formData = new FormData();
    
    // const uploadFile = () =>{
    //   axios.post('', formData, {
    //               headers: {
    //                 'Content-Type': 'multipart/form-data'
    //               }
    //             }
    //   )
    // }

    // const handleFileUpload = () => {
    //   this.file = this.$refs.file.files[0]
    //   formData.append('file', this.file);
    //   uploadFile()
    // }


    const toggleActive =  () => {
      active.value = !active.value; 
    }

    
    return {active, toggleActive};
  }
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