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
                <b-field class="has-text-light" label="." expanded>
                    <button class="button is-primary" @click="getClusters">Применить</button>
                </b-field>
            </b-field>
        </div>
        <div class="columns">
            <div v-for="cluster in clusters" class="column"> <!--Товар-->
                <h1 class="subtitle has-text-grey">Кластер {{ cluster['cluster_num'] }}</h1>
                <div class="column">
                    <div class="box">
                        <table class="table is-striped is-size-7">
                          <thead>
                            <tr>
                              <th><abbr title="Position">Артикул</abbr></th>
                              <th><abbr title="Played">Наименование</abbr></th>
                            </tr>
                          </thead>
                          <tbody>
                            <tr v-for="product in cluster['products'].slice(0,10)">
                                <td>{{ product['product'] }}</td>
                                <td>{{ product['product_name'] }}</td>
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
                clusters: [{cluster_num: 0, products: [{product: '', product_name: ''}]}],
            }
        },
        methods: {
            getClusters () {
                axios.get('http://127.0.0.1:5000/cluster/'.concat(this.selected)).then(response => {
                    this.clusters = response.data['clusters']
                })
            }
        }
    }
</script>

<style scoped>

</style>