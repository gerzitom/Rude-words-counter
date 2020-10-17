<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <Counter :words-count="wordsCount" :words="words" class="mb-6" @wordCountAdded="wordCountAdded" />
      <v-card class="rounded-lg outlined py-5  px-6">
        <p class="button mb-1">
          Částka k zaplacení
        </p>
        <v-row justify="space-between">
          <v-col cols="6">
            <p class="text-h4 font-weight-bold mb-0">
              {{ priceToPay }} Kč
            </p>
          </v-col>
          <v-col cols="auto">
            <v-btn @click="pricePayed">
              Vynulovat
            </v-btn>
          </v-col>
        </v-row>
      </v-card>
      <v-card class="rounded-lg outlined py-5 px-6 mt-6">
        <p class="button mb-1">
          Celkově zaplaceno
        </p>
        <v-row>
          <v-col cols="8">
            <p class="text-h4 font-weight-bold mb-0">
              {{ paid }} Kč
            </p>
          </v-col>
        </v-row>
      </v-card>
      <WordsList :words="words" />
    </v-col>
  </v-row>
</template>
<script>
import Counter from '~/components/Counter'
export default {
  components: {
    Counter,
    WordsList: () => import('~/components/RudeWordsList')
  },
  data () {
    return {
      words: [],
      paid: 0
    }
  },
  computed: {
    totalCount () {
      let total = 0
      this.words.forEach((word) => {
        total += word.price * word.count
      })
      return total
    },
    priceToPay () {
      return this.totalCount - this.paid
    },
    wordsCount () {
      let count = 0
      this.words.forEach((word) => {
        count += word.count
      })
      return count
    }
  },
  mounted () {
    this.$axios.get('/words')
      .then((response) => {
        this.words = response.data
      })
    this.$axios.get('/paied')
      .then((response) => {
        this.paid = response.data
      })
  },
  methods: {
    wordCountAdded (wordName) {
      this.words.forEach((word) => {
        if (word.name === wordName) { word.count++ }
      })
      // this.words[word].count++
    },
    pricePayed () {
      this.$axios.put('/paied', {
        price: this.priceToPay
      })
        .then((response) => {
          if (response.status === 200) {
            this.paid += this.priceToPay
          }
        })
    }
  }
}
</script>
