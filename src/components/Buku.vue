<template>
    <div id="Buku">
      <h5>Books</h5>
      <div class="row items-center justify-center">
        <div v-for="(item, index) in items" :key="index" class="my-card">
          <img :src="item.image" />
          <div class="buku-info">
            <div class="text-h6">{{ item.title }}</div>
            <div class="text-subtitle2">by {{ item.author }}</div>
          </div>
          <div class="q-pt-none">
            {{ item.description }}
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        items: [
        { image: '/assets/ForBook/LUKACITA.jpeg', title: 'LUKACITA'},
        { image: '/assets/ForBook/SERANGKAI.jpeg', title: 'SERANGKAI'},
        { image: '/assets/ForBook/ORIENT.jpeg', title: 'MURDER ON THE ORIENT EXPRESS'},
        { image: '/assets/ForBook/TheMajor.jpeg', title: 'The Major'},
        { image: '/assets/ForBook/bluemoon.jpeg', title: 'In a Blue Moon'}
        ]
      };
    }
  };
  </script>
  
  <style scoped>
  .my-card {
    width: 100%;
    max-width: 250px;
    border: 2px solid #ba1641;
    margin: 10px;
    padding: 10px;
  }
  
  h5 {
    color: #86153a;
    font-size: 1.5rem;
    font-weight: bold;
    margin-bottom: 1rem;
    text-align: center;
  }
  
  img {
    width: 100%;
    height: auto;
  }
  
  .text-h6 {
    font-size: 1.25rem;
    font-weight: bold;
  }
  
  .text-subtitle2 {
    font-size: 1rem;
    color: #777;
  }
  </style>
  