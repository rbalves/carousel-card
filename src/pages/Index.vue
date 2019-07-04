<template>
  <div class="q-pa-md">
    <div class="row text-center">
      <div class="col"></div>
      <div class="col-xs-3">
        <q-select v-model="filtro" :options="filtros" label="Cards por página"/>
      </div>
      <div class="col"></div>
    </div>
    <div class="q-pa-md row q-gutter-md">
      <div class="col"></div>
      <div class="col-xs-2" v-for="card in cardsFiltrados" :key="card">
        <q-card class="my-card">
          <q-card-section>
            <div class="text-h6">Title {{ card }}</div>
            <div class="text-subtitle2">by John Doe</div>
          </q-card-section>

          <q-card-section>
            {{ lorem }}
          </q-card-section>
        </q-card>
      </div>
      <div class="col"></div>
    </div>
    <div class="row text-center">
      <div class="col"></div>
      <div class="col-xs-4">
        <q-btn color="blue" label="Anterior" @click="voltar()" :disabled="cardInicio == 0" />
      </div>
      <div class="col-xs-4">
        <q-btn color="blue" label="Próximo" @click="avancar()" :disabled="cardInicio + filtro >= cards.length" />
      </div>
      <div class="col"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      cardInicio: 0,
      cards: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
      cardsFiltrados: [],
      filtro: 1,
      filtros: [1, 2, 3, 4, 5],
      lorem: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.'
    }
  },
  mounted () {
    this.filtrarCards(this.cardInicio)
  },
  watch: {
    filtro: function () {
      this.cardInicio = 0
      this.filtrarCards(this.cardInicio)
    }
  },
  methods: {
    voltar () {
      if (this.cardInicio > 0) {
        this.cardInicio -= this.filtro
        this.filtrarCards(this.cardInicio)
      }
    },
    avancar () {
      if (this.cardInicio + this.filtro < this.cards.length) {
        this.cardInicio += this.filtro
        this.filtrarCards(this.cardInicio)
      }
    },
    filtrarCards (cardInicio) {
      this.cardsFiltrados = []
      let cardFim = (this.cards.length - cardInicio >= this.filtro) ? cardInicio + this.filtro : this.cards.length
      for (let i = cardInicio; i < cardFim; i++) {
        this.cardsFiltrados.push(this.cards[i])
      }
    }
  }
}
</script>

<style scoped>
.my-card{
  width: 100%;
  max-width: 250px;
}
</style>
