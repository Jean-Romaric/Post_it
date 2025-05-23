<template class="bg-gradient-to-r from-cyan-500 to-blue-500">
  <div></div>
  <div
    class="max-w-sm p-6 bg-white border border-gray-200 rounded-lg shadow dark:bg-gray-800 dark:border-gray-700 mt-6 ml-6 display-flex"
  >
    <label for="title">Title: </label>

    <a href="#">
      <div
        class="max-w-sm p-6 bg-white border border-gray-200 rounded-lg shadow dark:bg-gray-800 dark:border-gray-700 mt-6 ml-6"
      >
        <a href="#">
          <h5
            class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white"
          >
            <input
              type="text"
              id="first_name"
              class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
              placeholder="John"
              required
              v-model="model.post.titre"
            />
          </h5>
        </a>
      </div>
    </a>
    <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">
      <label
        for="message"
        class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
        >Ton message</label
      >
      <textarea
        id="body"
        rows="6"
        class="block p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
        placeholder="Leave a comment..."
        v-model="model.post.description"
      ></textarea>
    </p>
    <button
      type="button"
      class="text-white bg-gradient-to-br from-green-400 to-blue-600 hover:bg-gradient-to-bl focus:ring-4 focus:outline-none focus:ring-green-200 dark:focus:ring-green-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2"
      @click="savePost"
    >
      Poster
    </button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      model: {
        post: {
          titre: "",
          description: "",
        },
      },
    };
  },
  methods: {
    savePost() {
      axios
        .post("https://post-it.epi-bluelock.bj/notes", {
          title: this.model.post.titre,
          content: [this.model.post.description],
        })
        .then((res) => {
          console.log(res.data);
          this.$router.push("/"); // redirige l'utilisateur vers la page d'accueil après la réussite de la requête POST
          // alert(res.data.message);
          this.model.post = {
            titre: " ",
            description: "",
          };
        });
    },
  },
};
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
}
textarea {
  border: solid 2px;
}
button {
  border: solid 2px;
}

div {
  margin: 24px auto;
}
label {
  font-weight: bolder;
  display: block;
  margin-bottom: 4px;
}
</style>
