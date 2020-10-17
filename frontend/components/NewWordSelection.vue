<template>
  <v-card>
    <v-card-title class="headline">
      Tom řekl sprosté slovo
    </v-card-title>
    <v-card-text>
      <v-btn
        v-for="word in words"
        :key="word.name"
        elevation="2"
        block
        class="my-2"
        @click="wordChosen(word.name)"
      >
        {{ word.name }}
      </v-btn>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  name: 'NewWordSelection',
  props: {
    words: {
      type: Array,
      default: null
    }
  },
  methods: {
    wordChosen (word) {
      this.$axios.put('/word', {
        word
      })
        .then((result) => {
          if (result.status === 200) {
            this.$emit('wordCountAdded', word)
          }
        })
    }
  }
}
</script>

<style scoped lang="scss">

</style>
