<template>
  <q-page class="flex column">
    <div class="col q-pt-lg q-px-md">
      <q-input
        v-model="search"
        placeholder="Поиск"
        borderless
        dark>
        <template v-slot:before>
          <q-icon name="my_location" />
        </template>
        <template v-slot:append>
          <q-btn round dense flat icon="search" />
        </template>
      </q-input>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      search: ''
    }
  }
}
</script>
<style lang="scss">
.q-page {
background: linear-gradient(to top, #0f0c29, #302b63, #24243e )
}
</style>
