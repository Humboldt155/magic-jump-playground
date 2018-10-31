<template>
  <div>
      <nav class="navbar is-transparent">
          <div class="navbar-brand ">
            <h1 class="subtitle has-text-grey-light is-size-4">Magic Jump <strong class="has-text-success">playground</strong></h1>
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
          <b-tab-item label="Предсказание по категориям">
              <categorical_predict></categorical_predict>
          </b-tab-item>
          <b-tab-item label="Кластеризация модели">
              <model_clusters></model_clusters>
          </b-tab-item>
          <b-tab-item label="Ближайшие проекты">
              <scatter></scatter>
          </b-tab-item>
      </b-tabs>

  </div>
</template>

<script>



import complementary from './components/complementary.vue'
import code_projects from './components/code_projects.vue'
import analogs from './components/analogs.vue'
import categorical_predict from './components/categorical_predict.vue'
import model_clusters from './components/model_clusters.vue'
import scatter from './components/scatter.vue'

export default {
  name: 'app',
  components: {
      complementary,
      code_projects,
      analogs,
      categorical_predict,
      model_clusters,
      scatter
  }
}
</script>

<style>

</style>
