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
                    <h1 class="title has-text-info is-size-4">Наиболее похожие товары: </h1>
                    <table class="table is-striped">
                      <thead>
                        <tr>
                          <th><abbr title="Position">Код</abbr></th>
                          <th><abbr title="Position">Фото</abbr></th>
                          <th><abbr title="Played">Наименование товара</abbr></th>
                          <th><abbr title="Won">Схожесть, %</abbr></th>
                          <th><abbr title="Won">Наименование модели Адео</abbr></th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr v-for="product in most_similar['similars']">
                            <td>{{ product.product }}</td>
                            <td>
                                <figure class="image is-128x128">
                                    <img :src="product.url"/>
                                </figure>
                            </td>
                            <td>{{ product.product_name }}</td>
                            <td>{{ product.probability }}</td>
                            <td>{{ product.model_name }}</td>
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
        name: "analogs",
        data () {
            return {
                selected: '18745342',
                qty: 100,
                most_similar: ''
            }
        },
        methods: {
            getAnalogs () {
                axios.get('http://127.0.0.1:5000/most_similar/'.concat(this.selected, '/', this.qty.toString())).then(response => {
                    this.most_similar = response.data
                })
            }
        }
    }
</script>

<style scoped>

</style>
