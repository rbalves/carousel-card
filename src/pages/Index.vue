<template>
  <div class="q-pa-md">
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
        <q-btn color="blue" label="Próximo" @click="avancar()" :disabled="cardInicio + 3 >= cards.length" />
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
      lorem: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.'
    }
  },
  mounted () {
    this.filtrarCards(this.cardInicio)
  },
  methods: {
    voltar () {
      if (this.cardInicio > 0) {
        this.cardInicio -= 3
        this.filtrarCards(this.cardInicio)
      }
    },
    avancar () {
      if (this.cardInicio + 3 < this.cards.length) {
        this.cardInicio += 3
        this.filtrarCards(this.cardInicio)
      }
    },
    filtrarCards (cardInicio) {
      this.cardsFiltrados = []
      let cardFim = (this.cards.length - cardInicio >= 3) ? cardInicio + 3 : this.cards.length
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
