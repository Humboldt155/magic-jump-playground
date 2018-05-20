<template>
    <section>
        <nav class="navbar is-transparent">
          <div class="navbar-brand ">
            <h1 class="subtitle has-text-grey-light is-size-3">Magic Jump <strong class="has-text-success">playground&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</strong></h1>
          </div>
            <div class="navbar-menu">
                <div class="navbar-start">
                  <div class="navbar-item">
                    <b-field>
                        <b-input placeholder="артикул" v-model="selected">
                        </b-input>
                        <p class="control">
                            <button class="button" @click="getComplementary(selected)">применить</button>
                        </p>
                      </b-field>
                  </div>
                  <div class="navbar-item">
                    <button class="button is-outlined" @click="clearBasket">Очистить корзину</button>
                  </div>
                </div>
            </div>
        </nav>
        <br>
        <br>
<!--------------------------Блок ЗАГОЛОВКОВ-------------------------------->
        <div class="columns">
            <div class="column is-one-third"> <!--Товар-->
                <h1 class="subtitle has-text-grey">Товар</h1>
            </div>
            <div class="column">
                <div class="columns">
                    <div class="column is-one-fifth">
                        <p class="has-text-primary is-size-5">С этим товаром покупают</p>
                    </div>
                    <div class="column is-one-fifth">
                        <p class="has-text-grey is-size-5">Товарная группа</p>
                    </div>
                    <div class="column">
                        <p class="has-text-grey is-size-5">Аналоги комплиментарных товаров</p>
                    </div>
                </div>
            </div>
        </div>
        <div class="columns">

<!--------------------------Карточка товара-------------------------------->
            <div class="column is-one-third"> <!--Товар-->
                <div class="box">
                    <h1 class="title has-text-primary is-size-4">Карточка товара: </h1>
                    <h1 class="is-size-4">
                        {{ complements.product_name }}
                    </h1><br>
                    <h2 class="is-size-5 has-text-grey">
                        {{ complements.product }}
                    </h2>
                    <br><br>
                    <br><br>
                </div>
<!--------------------------Блок АНАЛОГОВ-------------------------------->
                <div class="box">
                    <h1 class="title has-text-info is-size-4">Аналоги: </h1>
                    <table class="table is-striped">
                      <thead>
                        <tr>
                          <th><abbr title="Position">Код</abbr></th>
                          <th><abbr title="Played">Наименование товара</abbr></th>
                          <th><abbr title="Won">Схожесть, %</abbr></th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr v-for="prod in analogs.models[0]['products']">
                            <td>{{ prod.product }}</td>
                            <td>{{ prod.product_name }}</td>
                            <td>{{ Math.round(prod.probability * 100) / 100 }}</td>
                        </tr>
                      </tbody>
                    </table>
                </div>

<!--------------------------Блок КОРЗИНЫ-------------------------------->
                <div class="box">
                    <h1 class="title has-text-danger is-size-4">Корзина: </h1>
                    <table class="table is-striped">
                      <thead>
                        <tr>
                          <th><abbr title="Position">Код</abbr></th>
                          <th><abbr title="Played">Наименование товара</abbr></th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr v-for="basket_product in basket_products">
                            <td>{{ basket_product.product }}</td>
                            <td>{{ basket_product.product_name }}</td>
                        </tr>
                      </tbody>
                    </table>
                </div>
            </div>

<!--------------------------Блок КОМПЛЕМЕНТОВ-------------------------------->
            <div class="column">
                <div v-for="model in models.slice(0, 5)" class="container">
                    <div>

                        <div class="columns">
                            <div class="column is-one-fifth">
                                <div class="box">

                                    <p class="is-size-6 has-text-dark">{{ model.products[0].product_name }}</p><br>
                                    <p class="is-size-6 has-text-grey-light">Вероятность:&nbsp;&nbsp;<strong>{{ Math.round(model.products[0].probability * 1000000) / 1000000 }}  %</strong></p>
                                    <div class="is-size-6 has-text-grey-light">Арт: {{ model.products[0].product }}
                                        <button class="button is-danger is-outlined is-small"
                                                @click="add_to_basket({
                                                    product: model.products[0].product,
                                                    product_name: model.products[0].product_name,
                                                })">
                                            в корзину
                                        </button>
                                    </div>

                                    <button v-if="model.products[0].is_stm" class="button is-success is-small">
                                        СТМ
                                    </button>
                                </div>
                            </div>
                            <div class="column is-one-fifth">
                                <p class="has-text-grey is-size-6"><br>{{ model.model_name }}-----></p>
                            </div>
<!--------------------------Блок АНАЛОГОВ КОМПЛЕМЕНТОВ-------------------------------->
                            <div v-for="product in model.products.slice(1, 7)" class="column is-one-fifth">
                                <div class="box">

                                    <p class="is-size-6 has-text-grey">{{ product.product_name }}</p>
                                    <p class="is-size-7 has-text-grey">Вероятность: <strong>{{ Math.round(product.probability * 1000000) / 1000000 }}&nbsp;%</strong></p>
                                    <div class="is-size-7 has-text-grey">
                                        Арт: {{ product.product }}
                                        <button class="button is-danger is-outlined is-small"
                                                @click="add_to_basket({
                                                    product: product.product,
                                                    product_name: model.products[0].product_name,
                                                })">
                                            в корзину
                                        </button>
                                    </div>
                                    <button v-if="model.products[0].is_stm === 1" class="button is-success is-small">
                                        СТМ
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                    <br>
                </div>
                <div class="box">
                    <h1 class="title has-text-success is-size-4">За чем клиент придет в следующий раз: </h1>
                </div>
            </div>
        </div>
        <br>
        <hr>
    </section>
</template>

<script>
    import axios from 'axios';

    export default {
        name: "complementary",
        data () {
            return {
                selected: '',
                basket_products: [],
                basket_list: '',
                main_code: '123456789',
                main_name: 'Наименование основного товара',
                complements: {"models": [], "product": '',  "product_name": ''},
                analogs: {"models": [{products: ['']}]}
            }
        },
        methods: {
            getComplementary (products) {
                axios.get('http://127.0.0.1:5000/complementary/'.concat(products, this.basket_list, '/')).then(response => {
                    this.complements = response.data
                })
                axios.get('http://127.0.0.1:5000/analogs/'.concat(this.selected, '/')).then(response => {
                    this.analogs = response.data
                })
            },
            add_to_basket (product_object) {
                this.basket_list = this.basket_list.concat(',', product_object.product.toString())
                this.basket_products.push(product_object)
                this.getComplementary(this.selected.concat(this.basket_list))
            },
            clearBasket () {
                this.basket_list = ''
                this.basket_products = []
                this.getComplementary(this.selected)
            }
        },
        computed: {
            models () {
                return this.complements.models
            },
            img_path () {
                return 'https://s.leroymerlin.ru/upload/catalog/img/5/b/'.concat(this.selected, '/800x800/', this.selected,'.jpg')
            }
        }
    }
</script>

<style scoped>

</style>