<template>
  <div class="container">
    <div class="row">
      <div class="col-sm-10">
        <h1>Books</h1>
        <hr><br><br>
        <button type="button" class="btn btn-success btn-sm">Add Book</button>
        <br><br>
        <table class="table table-hover">
          <thead>
            <tr>
              <th scope="col">Title</th>
              <th scope="col">Author</th>
              <th scope="col">Read?</th>
              <th></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(book, index) in books" :key="index">
              <td>{{ book.title }}</td>
              <td>{{ book.author }}</td>
              <td>
                <span v-if="book.read">Yes</span>
                <span v-else>No</span>
              </td>
              <td>
                <div class="btn-group" role="group">
                  <button type="button" class="btn btn-warning btn-sm">Update</button>
                  <button type="button" class="btn btn-danger btn-sm">Delete</button>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      books: [],
    };
  },
  methods: {
    getBooks() {
      // ここでback-endエンドポイントを叩く　
      const path = 'http://localhost:5001/books';
      axios.get(path)
          .then((res) => {
            this.books = res.data.books;
          })
          .catch((error) => {
            console.error(error);
          });
    },
  },
  // > After the component is initialized, the getBooks method is called via the created lifecycle hook,
  // > which fetches the books from the back-end endpoint.
  created() {
    this.getBooks();
  }
};
</script>












