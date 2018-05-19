<template>
  <div class="section">
      <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="navbar-brand ">
        <h1 class="subtitle has-text-grey-light">Magic Jump playground</h1>
      </div>
    </nav>
      <div>
        <b-tabs type="is-boxed">
            <b-tab-item label="Аналоги" icon="google-photos">
                <analogs></analogs>
            </b-tab-item>
            <b-tab-item label="С этим товаром покупают" icon="library-music">
                <complementary></complementary>
            </b-tab-item>
            <b-tab-item label="Предложение на следующую покупку" icon="video">
                <forecast></forecast>
            </b-tab-item>
        </b-tabs>
      </div>
  </div>
</template>

<script>
import analogs from './components/analogs.vue'
import complementary from './components/complementary.vue'
import forecast from './components/forecast.vue'

export default {
  name: 'app',
  components: {
      analogs,
      complementary,
      forecast
  }
}
</script>

<style>

</style>
