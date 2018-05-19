<template>
    <section>
        <h1 class="title">Аналоги и Up-sale</h1>
        <h2 class="subtitle"></h2>
        <div class="columns"> <!--Блок корзины-->
          <div class="column">
            <button class="button is-primary is-outlined" @click="clearBasket">Очистить корзину</button>
              <br>
              <br>
              <br>
              <b-field>
                <b-input placeholder="артикул" v-model="selected">
                </b-input>
                <p class="control">
                    <button class="button is-primary" @click="getComplementary(selected)">применить</button>
                </p>
              </b-field>
          </div>

<!--------------------------КОРЗИНА-------------------------------------->
          <div class="column is-two-thirds">
              <div class="box">
                  <article class="media">
                      <figure class="media-left">
                          <p class="image is-128x128">
                              <img src="../assets/basket.png">
                           </p>
                      </figure>
                      <div class="media-content"><br>
                          <div class="columns">
                              <div v-for="basket_product in basket_products" class="column is-one-quarter">
                                  <div class="section">
                                  <div class="box">
                                      <p>{{ basket_product.product }}</p><br>
                                      <p><strong>{{ basket_product.product_name }}</strong></p><br>
                                  </div></div>
                              </div>
                          </div>
                      </div>
                  </article>
              </div>
          </div>
        </div>

<!--------------------------Блок ЗАГОЛОВКОВ-------------------------------->
        <div class="columns">
            <div class="column is-one-third"> <!--Товар-->
                <h1 class="title has-text-grey">Товар</h1>
            </div>
            <div class="column">
                <p class="title has-text-grey">С этим товаром покупают&nbsp;&nbsp;&nbsp;&nbsp;
                Аналоги комплементарных товаров</p>
            </div>
        </div>
        <br>
        <div class="columns">

<!--------------------------Карточка товара-------------------------------->
            <div class="column is-one-third"> <!--Товар-->
                <h1 class="subtitle has-text-primary">Карточка товара</h1>
                <div class="box">
                    <h1 class="title ">
                        {{ complements.product_name }}
                    </h1><br>
                    <h2 class="subtitle has-text-grey">
                        {{ complements.product }}
                    </h2>
                    <br><br><br><br><br><br><br><br>
                </div>
                <br>
                <br>

<!--------------------------Блок АНАЛОГОВ-------------------------------->

                <h1 class="title has-text-grey">Аналоги: </h1><br>
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
                        <td>{{ prod.probability }}</td>
                    </tr>
                  </tbody>
                </table>
            </div>

<!--------------------------Блок КОМПЛЕМЕНТОВ-------------------------------->
            <div class="column">
                <div v-for="model in models.slice(0, 5)" class="container">
                    <div>
                        <h1 class="subtitle has-text-primary">{{ model.model_name }}</h1>
                        <div class="columns">
                            <div class="column is-one-quarter">
                                <div class="box">
                                    <strong>{{ model.products[0].product }}</strong>&nbsp;
                                    <button v-if="model.products[0].is_stm" class="button is-primary is-primary is-small">
                                        СТМ
                                    </button>
                                    <p class="subtitle">{{ model.products[0].product_name }}</p>
                                    <p class="subtitle"><strong>Вероятность, %:</strong> {{ model.products[0].probability }}</p><br>
                                    <button class="button is-danger is-outlined is-small"
                                            @click="add_to_basket({
                                                product: model.products[0].product,
                                                product_name: model.products[0].product_name,
                                            })">
                                        в корзину
                                    </button>
                                </div>
                            </div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                            <div v-for="product in model.products.slice(1, 7)" class="column is-one-fifth">
                                <div class="box">
                                    <strong>{{ product.product }}</strong>&nbsp;
                                    <button v-if="model.products[0].is_stm === 1" class="button is-primary is-small">
                                        СТМ
                                    </button>
                                    <p class="subtitle has-text-primary">{{ product.product_name }}</p>
                                    <p class="subtitle"><strong>Вероятность, %: </strong>{{ product.probability }}</p><br>
                                    <button class="button is-danger is-outlined is-small"
                                            @click="add_to_basket({
                                                product: product.product,
                                                product_name: model.products[0].product_name,
                                            })">
                                        в корзину
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                    <br>
                    <br>
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
                selected: '18745334',
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
            }
        }
    }
</script>

<style scoped>

</style>