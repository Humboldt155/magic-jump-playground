<template>
    <section>
        <div class="columns">
            <b-field grouped>
                <b-field label="Артикул" expanded>
                    <b-field>
                        <b-input v-model="selected" placeholder="артикул" expanded></b-input>
                    </b-field>
                </b-field>
                <b-field label="Количество товаров" expanded>
                    <b-input v-model="qty" placeholder="количество"></b-input>
                </b-field>
                <b-field class="has-text-light" label="." expanded>
                    <button class="button is-primary" @click="getAnalogs">Применить</button>
                </b-field>
            </b-field>
        </div>
        <div class="columns">
            <div class="column">
                <div class="box">
                    <h1 class="title has-text-info is-size-4">Близкие категории: </h1>
                    <table class="table is-striped">
                      <thead>
                        <tr>
                          <th><abbr title="Position">Код</abbr></th>
                          <th><abbr title="Played">Наименование модели</abbr></th>
                          <th><abbr title="Won">Вероятность, %</abbr></th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr v-for="model in models">
                            <td>{{ model.model_adeo }}</td>
                            <td>{{ model.model_name }}</td>
                            <td>{{ model.probability }}</td>
                        </tr>
                      </tbody>
                    </table>
                </div>
            </div>
            <div class="column"></div>
        </div>
    </section>
</template>

<script>
    import axios from 'axios'

    export default {
        name: "categorical_predict",
        data () {
            return {
                selected: '18745342',
                qty: 20,
                models: ''
            }
        },
        methods: {
            getAnalogs () {
                axios.get('http://127.0.0.1:5000/categorical_predict/'.concat(this.selected, '/', this.qty.toString())).then(response => {
                    this.models = response.data
                })
            }
        }
    }
</script>

<style scoped>

</style>