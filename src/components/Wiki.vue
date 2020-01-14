<template>
  <div class="container">
    <h1>Wikipedia</h1>
    <div class="search">
      <div>
        <input
          id="uniqueSearch"
          class="unique-search"
          v-model.trim="uniqueSearch"
          type="search"
          placeholder="Buscar..."
          v-on:keyup.enter="searchData"
        />
      </div>
      <div>
        <a
          href="https://en.wikipedia.org/wiki/Special:Random"
          target="_blank"
          class="random-search btn btn-info"
        >Busqueda Aletoria</a>
      </div>
    </div>

    <div>
      <ul v-for="article in articles" v-bind:key="article.pageid">
        <a :href="page + article.pageid" target="_blank">
          <li class="content">
            <h4>
              <b>{{article.title}}</b>
            </h4>
            <hr />
            <p>{{article.extract}}</p>
          </li>
        </a>
      </ul>
    </div>
  </div>
</template>

<script>
const baseURL =
  "https://en.wikipedia.org//w/api.php?action=query&format=json&prop=extracts%7Cdescription%7Cpageimages&generator=search&exchars=500&exlimit=20&exintro=1&explaintext=1&gsrnamespace=*&gsrlimit=10&gsrsearch=";

export default {
  data() {
    return {
      uniqueSearch: "",
      articles: [],
      page: "https://en.wikipedia.org/?curid="
    };
  },
  methods: {
    searchData() {
      let url = `${baseURL}${this.uniqueSearch}`;
      console.log(url);

      this.$http
        .jsonp(url)
        .then(res => {
          console.log(res.body.query.pages);
          this.articles = res.body.query.pages;
        })
        .catch(err => {
          console.log(err);
        });

      this.uniqueSearch = "";
    }
  }
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css?family=Roboto+Slab:400,600,800&display=swap");

.container {
  font-family: "Roboto Slab", serif;
}
.search {
  padding: 10px 0 10px 0;
}
.unique-search {
  margin: 10px 0 10px 0;
  padding: 5px;
  border-radius: 15px;
}
.random-search {
  border-radius: 15px;
  margin: 10px 0 10px 0;
}
a {
  text-decoration: none;
  color: #ffffff;
}
h4 {
  padding-top: 15px;
}
p {
  padding: 0 15px 15px 15px;
}
.content {
  padding: 2px 16px;
  background-color: #0f4c75;
  margin: 10px;
}
li {
  list-style-type: none;
}
li:hover {
  border-left: 15px solid #1b262c;
  margin-left: -5px;
}
</style>