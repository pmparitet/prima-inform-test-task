<template>
  <main>
    <h1>Adress API from https://random-data-api.com/</h1>
    <v-data-table
      :headers="adressHeaders"
      :items="adressList"
      :expanded.sync="expanded"
      item-key="id"
      show-select
      show-expand
      class="elevation-3"
    >
      <template #top>
        <v-toolbar flat>
          <v-toolbar-title>Adress List</v-toolbar-title>
        </v-toolbar>
      </template>
      <template #expanded-item="{ headers, item }">
        <td :colspan="headers.length">
          Full address:  {{ item.full_address }}
        </td>
      </template>
    </v-data-table>
  </main>
</template>

<script>
export default {
  async asyncData ({ $axios }) {
    const adressList = await $axios.$get('https://random-data-api.com/api/address/random_address?size=5')
      .catch((error) => { console.log('Ошибка:', error) })
    return { adressList }
  },
  data () {
    return {
      expanded: [],
      adressHeaders: [
        { text: 'ID', align: 'start', sortable: false, value: 'id' },
        { text: 'Time zone', value: 'time_zone' },
        { text: 'City', value: 'city' },
        { text: 'Address', value: 'street_address' },
        { text: '', value: 'data-table-expand' }
      ]
    }
  }
}
</script>
