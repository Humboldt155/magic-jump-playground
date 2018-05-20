<template>
  <div class="section">
      <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="navbar-brand ">
        <h1 class="subtitle has-text-grey-light is-size-2">Magic Jump playground</h1>
      </div>
    </nav>
      <div>
        <complementary></complementary>
      </div>
  </div>
</template>

<script>
import complementary from './components/complementary.vue'

export default {
  name: 'app',
  components: {
      complementary
  }
}
</script>

<style>

</style>
