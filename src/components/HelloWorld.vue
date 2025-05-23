<template>
  <div></div>
  <div class="grid grid-cols-4 gap-4">
    <div v-for="note in notes" :key="note.id">
      <div
        class="max-w-sm p-6 bg-white border border-gray-200 rounded-lg shadow dark:bg-gray-800 dark:border-gray-700 mt-6 ml-6"
      >
        <a href="#">
          <div
            class="max-w-sm p-6 bg-white border border-gray-200 rounded-lg shadow dark:bg-gray-800 dark:border-gray-700 mt-6 ml-6"
          >
            <a href="#">
              <h5
                class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white"
              >
                {{ note.title }}
              </h5>
            </a>
          </div>
        </a>
        <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">
          {{ note.content[0] }}
        </p>
        <button
          type="button"
          class="text-white bg-gradient-to-br from-green-400 to-blue-600 hover:bg-gradient-to-bl focus:ring-4 focus:outline-none focus:ring-green-200 dark:focus:ring-green-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2"
          v-on:click="deleter(note._id)"
        >
          Supprimer
        </button>
        <button
          type="button"
          class="text-white bg-gradient-to-br from-green-400 to-blue-600 hover:bg-gradient-to-bl focus:ring-4 focus:outline-none focus:ring-green-200 dark:focus:ring-green-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2"
          v-on:click="modifier(note._id)"
        >
          Modifier
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
//const element = "";
export default {
  data() {
    return {
      notes: [],
    };
  },
  mounted() {
    axios.get("https://post-it.epi-bluelock.bj/notes").then((response) => {
      //tada tb d'objet
      //console.log(response);
      this.notes = response.data.notes;
    });
  },
  methods: {
    async getMetadata() {
      axios.get("https://post-it.epi-bluelock.bj/notes").then((response) => {
        this.notes = response.data.notes;
      });
      //console.log(this.notes);
    },

    deleter(id) {
      //if (confirm("Est tu sure de vouloir suprimer"))
      axios.delete(`https://post-it.epi-bluelock.bj/notes/${id}`).then(() => {
        this.getMetadata();
      });
      // .catch((error) => {
      //   element.parentElement.innerHTML = `Error: ${error.message}`;
      //   console.error("There was an error!", error);
      // });
    },
    modifier(id) {
      axios.put(`https://post-it.epi-bluelock.bj/notes/${id}`).then(() => {
        this.getMetadata();
      });
    },
  },
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
