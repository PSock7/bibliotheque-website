<!-- 
@author : Caleb akoa , Stael Douanla, Pape Mouhamadou Sock -->
<template>
  <div class="container">
    <article v-for="article in articles" :key="article.id">
      <div class="article-img">
        <div>
          <div :style="{ backgroundImage: 'url(' + article.image + ')' }"></div>
        </div>
      </div>

      <div class="article-content" v-if="editingArticle.id !== article.id">
        <div class="article-title">
          <h2>{{ article.name }} - {{ article.price }}€</h2>
          <div>
            <button
              v-if="!isInPanier(article.id)"
              @click="addToPanier(article.id)"
            >
              Ajouter au panier
            </button>
            <button v-else @click="removeFromPanier(article.id)">
              Retirer du panier
            </button>
            <button @click="deleteArticle(article.id)">Supprimer</button>
            <button @click="editArticle(article)">Modifier</button>
          </div>
        </div>
        <p>{{ article.description }}</p>
      </div>
      <div class="article-content" v-else>
        <div class="article-title">
          <h2>
            <input type="text" v-model="editingArticle.name" /> -
            <input type="number" v-model="editingArticle.price" />
          </h2>
          <div>
            <button @click="sendEditArticle()">Valider</button>
            <button @click="abortEditArticle()">Annuler</button>
          </div>
        </div>
        <p><textarea v-model="editingArticle.description"></textarea></p>
        <input
          type="text"
          v-model="editingArticle.image"
          placeholder="Lien vers l'image"
        />
      </div>
    </article>
    <button @click="showForm = !showForm">Ajouter un article</button>
    <add-article :show="showForm" @create-article="addArticle"></add-article>
  </div>
</template>

<script>
const AddArticle = window.httpVueLoader("./components/AddArticle.vue");

module.exports = {
  components: {
    AddArticle,
  },
  props: {
    articles: { type: Array, default: [] },
    panier: { type: Object },
  },
  data() {
    return {
      showForm: false,
      editingArticle: {
        id: -1,
        name: "",
        description: "",
        image: "",
        price: 0,
      },
    };
  },
  methods: {
    isInPanier(articleId) {
      return !!this.panier.articles.find((a) => a.id === articleId);
    },
    addToPanier(articleId) {
      this.$emit("add-to-panier", articleId);
    },
    removeFromPanier(articleId) {
      this.$emit("remove-from-panier", articleId);
    },
    addArticle(article) {
      this.$emit("add-article", article);
    },
    deleteArticle(articleId) {
      this.$emit("delete-article", articleId);
    },
    editArticle(article) {
      this.editingArticle.id = article.id;
      this.editingArticle.name = article.name;
      this.editingArticle.description = article.description;
      this.editingArticle.image = article.image;
      this.editingArticle.price = article.price;
    },
    sendEditArticle() {
      this.$emit("update-article", this.editingArticle);
      this.abortEditArticle();
    },
    abortEditArticle() {
      this.editingArticle = {
        id: -1,
        name: "",
        description: "",
        image: "",
        price: 0,
      };
    },
  },
};
</script>

<style scoped>
article {
 width: 750px;
  height: 423px;
  margin: 80px auto;
  background: #FFFFFF;
  box-shadow: 1px 2px 3px 0px rgba(0,0,0,0.10);
  border-radius: 6px;
 
  display: flex;
  flex-direction: column;
}

.img {
  margin-right: 50px;
}

.article-img div {
  width: 150px;
  height: 150px;
  background-size: cover;
}

.article-content {
   padding: 20px 30px;
  height: 120px;
  display: flex;
 
}

.article-title {
  height: 60px;
  padding: 20px 30px;
  color: #5E6977;
  font-size: 18px;
  font-weight: 400;
}

textarea {
  width: 100%;
}
</style>
