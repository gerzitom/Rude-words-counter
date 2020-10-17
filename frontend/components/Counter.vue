<template>
  <div class="counter">
    <p class="font-weight-regular text-uppercase overline mb-1">
      Tomášek řekl
    </p>
    <v-row
      align="center"
    >
      <v-col cols="8">
        <p class="text-h1 font-weight-medium mb-0">
          {{ wordsCount }}
        </p>
      </v-col>
      <v-col cols="4">
        <v-dialog
          v-model="displayOverlay"
          persistent
          max-width="300"
        >
          <template v-slot:activator="{on, attrs}">
            <v-btn
              x-large
              v-bind="attrs"
              v-on="on"
            >
              <v-icon>
                mdi-plus
              </v-icon>
            </v-btn>
          </template>
          <new-word-selection :words="words" v-on="$listeners" @wordCountAdded="wordCountAdded" />
        </v-dialog>
      </v-col>
    </v-row>
    <p class="text-h5">
      Sprostých slov
    </p>
  </div>
</template>

<script>
export default {
  name: 'Counter',
  components: {
    NewWordSelection: () => import('~/components/NewWordSelection')
  },
  props: {
    wordsCount: {
      type: Number,
      default: 0
    },
    words: {
      type: Array,
      default: null
    }
  },
  data () {
    return {
      displayOverlay: false
    }
  },
  methods: {
    wordCountAdded (wordName) {
      this.displayOverlay = false
    }
  }
}
</script>

<style scoped lang="scss">

</style>
