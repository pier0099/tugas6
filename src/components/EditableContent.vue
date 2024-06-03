<template>
    <div class="background">
      <div class="container">
        <h1>Jumlah Pahala</h1>
        <textarea v-model="inputContentTop" placeholder="Masukan Jumlah Pahala"></textarea>
        <textarea v-model="inputContent" placeholder="Kategori"></textarea>
        <button @click="saveContent">Save</button>
        <div v-if="savedContents.length">
          <h2>Ini Konten:</h2>
          <div v-for="(content, index) in savedContents" :key="index">
            <ContentItem 
              :content="content" 
              :index="index" 
              @update-content="updateContent" 
              @delete-content="deleteContent" 
            />
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import ContentItem from './ContentItem.vue';
  
  export default {
    components: {
      ContentItem
    },
    data() {
      return {
        inputContent: '',
        inputContentTop: '',
        savedContents: []
      };
    },
    methods: {
      saveContent() {
        if (this.inputContentTop.trim() && this.inputContent.trim()) {
          this.savedContents.push(this.inputContentTop);
          this.savedContents.push(this.inputContent);
          this.inputContent = '';
          this.inputContentTop = '';
        } else {
          alert('Konten tidak boleh kosong!');
        }
      },
      updateContent(index, newContent) {
        this.savedContents.splice(index, 1, newContent);
      },
      deleteContent(index) {
        this.savedContents.splice(index, 1);
      }
    }
  };
  </script>
  
  <style scoped>
  .background {
    width: 100vw;
    height: 100vh;
    background-image: url('/gambar/2.jpg');
    background-size: cover;
    background-position: center;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .container {
    width: 90%;
    max-width: 600px;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    text-align: left;
  }
  
  textarea {
    width: 100%;
    height: 30px;
    padding: 10px;
    margin-bottom: 20px;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-family: inherit;
    font-size: 14px;
  }
  
  button {
    padding: 10px 20px;
    background-color: #000000;
    color: #f4f4f4;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  button:hover {
    background-color: #4011d8;
  }
  
  h1 {
    margin-bottom: 20px;
    font-size: 24px;
    color: #333;
  }
  
  h2 {
    margin-top: 40px;
    font-size: 20px;
    color: #333;
  }
  </style>
  