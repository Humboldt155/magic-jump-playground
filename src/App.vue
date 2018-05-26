<template>
  <div>
      <nav class="navbar is-transparent">
          <div class="navbar-brand ">
            <h1 class="subtitle has-text-grey-light is-size-3">Magic Jump <strong class="has-text-success">playground</strong></h1>
          </div>
        </nav>
      <b-tabs position="is-centered">
          <b-tab-item label="Аналоги, комплименты товара">
              <complementary></complementary>
          </b-tab-item>
          <b-tab-item label="Проекты товара">
              <code_projects></code_projects>
          </b-tab-item>
          <b-tab-item label="Похожие товары">
              <analogs></analogs>
          </b-tab-item>
      </b-tabs>

  </div>
</template>

<script>
import complementary from './components/complementary.vue'
import code_projects from './components/code_projects.vue'
import analogs from './components/analogs.vue'

export default {
  name: 'app',
  components: {
      complementary,
      code_projects,
      analogs
  }
}
</script>

<style>

</style>
