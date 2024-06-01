<template>
  <div id="Main">
    <header>
      <Navbar />
      
    </header>
    <form @submit.prevent="save" class="form">
      <input type="text" v-model="form.title" placeholder="Judul" class="input" />
      <input type="text" v-model="form.content" placeholder="Penulis" class="input" />
      <button type="submit" class="button">Save</button>
    </form>
    <div class="table-container">
      <table class="table">
          <thead>
            <tr>
              <th>Judul Buku</th>
              <th>Nama Penulis</th>
              <th>Aksi</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="article in articles" :key="article.id">
              <td>{{ article.title }}</td>
              <td>{{ article.content }}</td>
              <td>
                <button @click="edit(article)" class="action-button">Edit</button>
                <button @click="deleteArticle(article)" class="action-button">Hapus</button>
              </td>
            </tr>
          </tbody>
        </table>
       
    </div>
   
    <button @click="load" class="button">Load</button><br />
    <Buku />
  </div>
</template>

<script>
import { ref, onMounted, reactive } from 'vue';
import axios from 'axios';
import Navbar from './components/Navbar.vue';
import Buku from './components/Buku.vue'

export default {

  components: {
    Navbar,
    Buku
  },

  setup() {
    const form = reactive({
      id: null,
      title: '',
      content: '',
    });

    const articles = ref([]);

    async function load() {
      try {
        const response = await axios.get('http://localhost:3000/articles');
        articles.value = response.data;
      } catch (error) {
        console.error('Error loading articles:', error);
      }
    }

    async function save() {
      try {
        const url = form.id
          ? `http://localhost:3000/articles/${form.id}`
          : 'http://localhost:3000/articles';
        const method = form.id ? 'put' : 'post';
        const response = await axios[method](url, form);

        if (form.id) {
          
          articles.value = articles.value.map((article) =>
            article.id === response.data.id ? response.data : article
          );
        } else {
          
          articles.value.push(response.data);
        }

      
        form.id = null;
        form.title = '';
        form.content = '';
      } catch (error) {
        console.error('Error saving article:', error);
      }
    }

    function edit(article) {
      form.id = article.id;
      form.title = article.title;
      form.content = article.content;
    }

    async function deleteArticle(article) {
      try {
        const response = await axios.delete(
          `http://localhost:3000/articles/${article.id}`
        );

        
        articles.value = articles.value.filter((item) => item.id !== article.id);
      } catch (error) {
        console.error('Error deleting article:', error);
      }
    }

    onMounted(load);

    return { form, articles, save, edit, load, deleteArticle };
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Rubik:wght@300;400;500;600;700;800&display=swap");
  
body{
  background-color: #fae5da;
}

header {
    padding-bottom: 100px;
}

.form {
  margin-bottom: 20px;
}

.table-container {
  overflow-x: auto;
}

.input {
  padding: 5px;
  margin-right: 10px;
  width: 200px;
}

.button {
  padding: 5px 10px;
  background-color: #e48d85; 
  color: white;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s; 
}

.button:hover {
  background-color: #d6675d; 
}

.table {
  width: 90vw;
  border-collapse: collapse;
}

th, td {
  border: 2px solid #e48d85;
  padding: 8px;
  text-align: center;
}

th {
  background-color: #e48d85; 
}

.action-button {
  padding: 3px 8px;
  margin-right: 5px;
  background-color: #e48d85; 
  color: white;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s; 
}

.action-button:hover {
  background-color: #d6675d; 
}
</style>
