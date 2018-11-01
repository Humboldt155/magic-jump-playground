<template>
    <section>
        <div class="columns">
            <div class="column is-one-quarter">
                <div class="columns">
                    <div class="column">
                        <b-field label="Число уровней">
                            <b-select
                                multiple
                                native-size="4"
                                size="is-small"
                                v-model="cycles">
                                <option value="2">  2 уровня</option>
                                <option value="3">  3 уровня</option>
                                <option value="4">  4 уровня</option>
                                <option value="5">  5 уровней</option>
                            </b-select>
                        </b-field>
                    </div>
                    <div class="column">
                        <b-field label="Код артикула или модели">
                            <b-input v-model="item"></b-input>
                        </b-field>
                        <b-field label="Что анализируем">
                            <b-select
                                multiple
                                native-size="2"
                                size="is-small"
                                v-model="type">
                                <option value="products">  Артикул</option>
                                <option value="models">  Модель</option>
                            </b-select>
                        </b-field>
                    </div>
                </div>
                <br>
                <button class="button is-primary" @click="getScatter">Применить</button>
            </div>
            <div class="column">
                <div class="box" style="min-height: 600px; top: 5px; position: relative; padding: 20px">
                    <div v-for="i in resp.reverse()" :style="{position: 'absolute', top: i.tsne_1*80+5+'%', left: i.tsne_2*72+3+'%'}">
                        <div class="button is-small is-rounded" :style="{backgroundColor: colors[i.rang], opacity: alpha[i.rang]}">
                            {{ i.model_name }}
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>

import axios from 'axios'

export default {
    name: "scatter",
    data () {
        return {
            resp: ['nothing'],
            item: 'MOD_200873',
            type: ['models'],
            cycles: ["3"],
            top_n_main: 15,
            top_n_sub: 5,
            iterations: 300,
            lr: 1,
            perplexity: 10,
            colors: {
                1: '#00bf06',
                2: '#d8f27a',
                3: '#c9c9c3',
                4: '#e8e8e1',
                5: '#e0dde2'
            },
            alpha: {
                1: 0.9,
                2: 0.8,
                3: 0.7,
                4: 0.4,
                5: 0.4
            }
        }
    },
    methods: {
        getScatter () {
            axios.get('http://127.0.0.1:5000/scatter', {
                params: {
                    item: this.item,
                    type: this.type[0],
                    cycles: this.cycles[0],
                    top_n_main: this.top_n_main,
                    top_n_sub: this.top_n_sub,
                    iterations: this.iterations,
                    lr: this.lr,
                    perplexity: this.perplexity
                }
            })
                .then(response => {
                    this.resp = response.data
            })
        }
    }
}
</script>

<style scoped>

</style>
