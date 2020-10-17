<template>
  <v-card class="rounded-lg outlined py-5 px-6 mt-6">
    <v-simple-table>
      <template v-slot:default>
        <thead>
          <tr>
            <th>
              Sprostá slova
            </th>
            <th>
              Cena
            </th>
            <th>
              Počet
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="word in words" :key="word.name">
            <td>
              {{ word.name }}
            </td>
            <td>{{ word.price }}</td>
            <td>{{ word.count }}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </v-card>
</template>

<script>
export default {
  name: 'RudeWordsList',
  props: {
    words: Array
  }
}
</script>

<style scoped lang="scss">

</style>
