<template>
  <div class="home">
    <!-- прелоадер -->
    <Preloader v-if="loading" />
    <!-- списки ссылок -->
    <div v-else class="wrapper-links">
      <ul v-for="(item, index) in arrs" :key="index" class="bg-list">
        <!-- li template -->
        <ItemLink
          class="bg-list__item"
          v-for="(item, index) in arrs[index]"
          :key="index"
          :textUrl="item.name"
          :urlLink="item.url"
        />
      </ul>
    </div>
    <!-- btns macros -->
    <div class="wrapper-macros">
      <button class="btn-preset" @click="handlerOpenPresetLinksJob">
        Preset Job
      </button>
    </div>
  </div>
</template>

<script>
// components
import ItemLink from "@/components/ItemLink.vue";
import Preloader from "@/components/Preloader.vue";
// links для macros job
import arrayLinks from "@/macros/macros.job.js";

export default {
  name: "App",
  //
  components: { ItemLink, Preloader },
  //
  data: () => ({
    loading: true,
    arrs: [],
    arrayMacrosJob: arrayLinks,
  }),
  //
  methods: {
    getData() {
      // список имен url
      let names = ["job", "it", "vue%20road"];

      let requests = names.map((name) =>
        fetch(`https://it-words-f02a9-default-rtdb.firebaseio.com/${name}.json`)
      );

      Promise.all(requests)
        .then((responses) => {
          return responses;
        })

        // преобразовать массив ответов response в response.json(),
        // чтобы прочитать содержимое каждого
        .then((responses) => Promise.all(responses.map((r) => r.json())))
        // все JSON-ответы обработаны
        .then((item) => (this.arrs = item))
        // если массив пустой, то лоадер
        .then((item) => (this.loading = item < 0 ? true : false));
    },

    // метод для открытия сразу нескольких ссылок, принимает массив
    macrosOpenLinksPreset(array) {
      array.forEach((item) => window.open(item));
    },
    // preset job links
    handlerOpenPresetLinksJob() {
      this.macrosOpenLinksPreset(this.arrayMacrosJob);
    },
  },
  mounted() {
    this.getData();
  },
};
</script>

<style>
/* style component */
.wrapper-links {
  padding: 5px;
  padding-top: 5%;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
}
.bg-list {
  background: #f9f8a8;
  box-shadow: 5px 5px 15px #000;
  margin: 15px;
  border-radius: 5px;
}
.bg-list__item {
  padding: 12px;
  width: 250px;
  text-align: center;
}

/* btn */
.btn-preset {
  background: #4fc08d;
  border: 1px solid;
  border-radius: 5px;
  font: inherit;
  padding: 0.75em 2em;
  cursor: pointer;
  color: #fff;
}
.btn-preset:hover {
  color: #4fc08d;
  transition: 0.5s;
  background: #fff;
}

/*  */
.wrapper-macros {
  display: flex;
  justify-content: center;
  margin-top: 25px;
}
</style>
