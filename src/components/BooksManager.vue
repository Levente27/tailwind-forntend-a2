<script setup>
import { createBook, getBooks } from '../api/books';
</script>

<script>
export default {
  name: "BooksManager",

  data() {
    return {
      books: [],
      newBook: {
        title: "",
        author: "",
        year: 2000,
      },
    };
  },


  mounted(){
    this.loadBooks();
  },

  methods: {
    async loadBooks() {
        this.books = await getBooks();
    },

    async addBooks(book){
        await createBook(book)
        await this.loadBooks();
    },

    async submitCreateBook(){
        await this.addBooks(this.newBook)
    }
  },
};
</script>

<template>
  <main class="">
    <h1 class="">Könyv kezelő rendszer</h1>


    <form @submit.prevent="submitCreateBook" class="border-2 border-stone-200 p-2 m-2 flex flex-col gap-4">
        <div class="flex flex-col">
            <label for="title">Cím:</label>
            <input v-model="newBook.title" type="text" class="border-2 border-stone-200" p-1 name="title">
        </div>

        <div class="flex-col">
            <label for="author">Szerző:</label>
            <input v-model="newBook.author" type="text" class="border-2 border-stone-200 p-1" name="author">
        </div>

        <div class="flex-col">
            <label for="year">Év:</label>
            <input v-model="newBook.year" type="number" class="border-2 border-stone-200 p-1" name="year">
        </div>

        <button class="border-2 border-stone-200 p-2" type="submit">Létrehozás</button>
    </form>


    <table class="">
      <thead class="">
        <tr>
          <th class="">azonosító</th>
          <th class="">cím</th>
          <th class="">szerző</th>
          <th class="">év</th>
          <th class="">műveletek</th>
        </tr>
      </thead>
      <tbody class="">
        <tr v-for="book in books" :key="book.id" class="">
            <td class="">{{ book.id }}</td>
            <td class="">{{ book.title }}</td>
            <td class="">{{ book.author }}</td>
            <td class="">{{ book.year }}</td>
            <td class="">-</td>
        </tr>
      </tbody>
    </table>
  </main>
</template>
