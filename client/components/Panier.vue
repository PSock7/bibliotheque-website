<!-- 
@author : Caleb akoa , Stael Douanla, Pape Mouhamadou Sock -->
<template>
  <div>
    <h2>Mon Panier</h2>
    <article v-for="article in panier.articles" :key="article.id">
      <div class="article-img">
        <div :style="{ backgroundImage: 'url(' + find(article).image + ')' }">
        </div>
      </div>
      <div class="article-content">
        <div class="article-title">
          <h2>{{ find(article).name }} - {{ find(article).price }}€
            <input type="number" :value="article.quantity" min="1" @change="changeQuantity(article.id, $event)">
          </h2>
        </div>
        <p>{{ find(article).description }}</p>
      </div>
    </article>
  </div>
</template>

<script>
module.exports = {
  props: {
    articles: { type: Array, default: [] },
    panier: { type: Object }
  },
  data () {
    return {
    }
  },
  async mounted () {
  },
  methods: {
    find (article) {
      return this.articles.find(a => a.id === article.id)
    },
    changeQuantity (articleId, { target: { value } }) {
      value = parseInt(value)
      this.$emit('change-quantity', { articleId, quantity: value })
    }
  }
}
</script>

<style scoped>
article {
  display: flex;
}

.article-img {
  flex: 1;
}

.article-img div {
  width: 100px;
  height: 100px;
  background-size: cover;
}

.article-content {
  flex: 3;
}

.article-title {
  display: flex;
  justify-content: space-between;
}

textarea {
  width: 100%;
}
</style>
