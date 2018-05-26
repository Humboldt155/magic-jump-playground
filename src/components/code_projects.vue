<template>
    <section>
        <div class="columns">
            <b-field grouped>
                <b-field label="Артикул" expanded>
                    <b-field>
                        <b-input v-model="selected" placeholder="артикул" expanded></b-input>
                    </b-field>
                </b-field>
                <b-field label="Число кластеров" expanded>
                    <b-input v-model="num_clusters" placeholder="количество кластеров"></b-input>
                </b-field>
                <b-field label="Макс артикулов в кластере" expanded>
                    <b-input v-model="max_products" placeholder="число артикулов макс"></b-input>
                </b-field>
                <b-field label="Всего продуктов" expanded>
                    <b-input v-model="total_products_qty" placeholder="всего продуктов"></b-input>
                </b-field>
                <b-field class="has-text-light" label="." expanded>
                    <button class="button is-primary" @click="getClusters">Применить</button>
                </b-field>
            </b-field>
        </div>
        <br>
        <br>
        <div class="columns">
            <div v-for="cluster in clusters" class="column"> <!--Товар-->
                <h1 class="subtitle has-text-grey">Кластер {{ cluster['cluster_num'] }}</h1>
                <div class="column">
                    <div class="box">
                        <table class="table is-striped is-size-6">
                          <tbody>
                            <tr v-for="product in cluster['products'].slice(0,max_products)">
                                <td>
                                    <p class="is-size-4 has-text-grey-darker">{{ product['product_name'] }}</p><br>
                                    <p class="is-size-6 has-text-grey">Вероятность: <strong class="is-size-6 has-text-grey">{{ Math.round(product.probability * 100000) / 1000 }}&nbsp;%</strong></p>
                                    <p class="is-size-6 has-text-grey">{{ product['product'] }}</p>
                                </td>
                            </tr>
                          </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>

    import axios from 'axios';

    export default {
        name: "code_projects",
        data () {
            return {
                selected: '18745342',
                max_products: 10,
                num_clusters: 5,
                total_products_qty: 5,
                clusters: [{cluster_num: 0, products: [{product: '', product_name: ''}]}],
            }
        },
        methods: {
            getClusters () {
                axios.get('http://127.0.0.1:5000/cluster/'.concat(
                    this.selected,
                    '/', this.num_clusters.toString(),
                    '/', this.total_products_qty.toString(),
                    '/', this.max_products.toString()))
                    .then(response => {
                    this.clusters = response.data['clusters']
                })
            }
        }
    }
</script>

<style scoped>

</style>