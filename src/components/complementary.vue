<template>
    <section>
        <h1 class="title">С этим товаром покупают</h1>
        <h2 class="subtitle"></h2>
        <div class="columns"> <!--Блок корзины-->
          <div class="column">
            <button class="button is-primary is-outlined">Начать сначала</button>
          </div>

          <!--Корзина-->
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
                              &nbsp;
                              <div class="column is-one-third">
                                  <div class="box">

                                      <p><strong>Название товара на русском языке</strong></p>
                                      <p>12345678</p>
                                      <button class="button is-warning is-outlined is-small">удалить</button>
                                  </div>
                              </div>
                              &nbsp;
                              <div class="column is-one-third">
                                  <div class="box">
                                      <p><strong>Название товара на русском языке</strong></p>
                                      <p>12345678</p>
                                      <button class="button is-warning is-outlined is-small">удалить</button>
                                  </div>
                              </div>
                              &nbsp;
                          </div>
                      </div>
                  </article>
              </div>
          </div>
        </div>

        <div class="columns"> <!--Блок карточки и главных комплементов-->
            <div class="column is-one-quarter"> <!--Товар-->
                <strong>Находимся в карточке этого товара</strong>
            </div>
            <div class="column is-one-fifth">С этим товаром покупают (видимый блок)</div>
            <div class="column">Аналоги комплементарных товаров</div>
        </div>

        <div class="columns"> <!--Блок карточки и главных комплементов-->
            <div class="column is-one-quarter"> <!--Товар-->
                <div class="box">
                    <h1 class="title ">
                        {{ main_name }}
                    </h1><br>
                    <h2 class="subtitle has-text-grey">
                        {{ main_code }}
                    </h2>
                    <br><br><br><br><br><br><br><br>
                </div>
            </div>
            <div class="column">
                <div class="columns">
                    <div class="column is-one-fifth">
                        <div class="box">
                            <strong>12345678</strong>&nbsp;
                            <button class="button is-primary is-primary is-small">СТМ</button>
                            <p>Название товара на русском языке 1</p><br>
                            <button class="button is-danger is-outlined is-small">в корзину</button>
                        </div>
                    </div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                    <div class="column is-one-fifth">
                        <div class="box">
                            <strong>12345678</strong>&nbsp;
                            <button class="button is-primary is-primary is-small">СТМ</button>
                            <p>Название товара на русском языке 1</p><br>
                            <button class="button is-danger is-outlined is-small">в корзину</button>

                        </div>
                    </div>
                    <div class="column is-one-fifth">
                        <div class="box">
                            <p><strong>12345678</strong></p>
                            <p>Название товара на русском языке 1</p><br>
                            <button class="button is-danger is-outlined is-small">в корзину</button>
                        </div>
                    </div>
                    <div class="column is-one-fifth">
                        <div class="box">
                            <p><strong>12345678</strong></p>
                            <p>Название товара на русском языке 1</p><br>
                            <button class="button is-danger is-outlined is-small">в корзину</button>
                        </div>
                    </div>
                    <div class="column is-one-fifth">
                        <div class="box">
                            <p><strong>12345678</strong></p>
                            <p>Название товара на русском языке 1</p><br>
                            <button class="button is-danger is-outlined is-small">в корзину</button>
                        </div>
                    </div>
                </div>
                <br>
                <br>
                <div class="columns">
                    <div class="column is-one-fifth">
                        <div class="box">
                            <p><strong>12345678</strong></p>
                            <p>Название товара на русском языке 1</p><br>
                            <button class="button is-danger is-outlined is-small">в корзину</button>
                        </div>
                    </div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                    <div class="column is-one-fifth">
                        <div class="box">
                            <strong>12345678</strong>&nbsp;
                            <button class="button is-primary is-primary is-small">СТМ</button>
                            <p>Название товара на русском языке 1</p><br>
                            <button class="button is-danger is-outlined is-small">в корзину</button>

                        </div>
                    </div>
                    <div class="column is-one-fifth">
                        <div class="box">
                            <p><strong>12345678</strong></p>
                            <p>Название товара на русском языке 1</p><br>
                            <button class="button is-danger is-outlined is-small">в корзину</button>
                        </div>
                    </div>
                    <div class="column is-one-fifth">
                        <div class="box">
                            <p><strong>12345678</strong></p>
                            <p>Название товара на русском языке 1</p><br>
                            <button class="button is-danger is-outlined is-small">в корзину</button>
                        </div>
                    </div>
                    <div class="column is-one-fifth">
                        <div class="box">
                            <p><strong>12345678</strong></p>
                            <p>Название товара на русском языке 1</p><br>
                            <button class="button is-danger is-outlined is-small">в корзину</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
    export default {
        name: "complementary",
        data () {
            return {
                main_code: '123456789',
                main_name: 'Наименование основного товара'
            }
        },
        methods: {
            getAnalogs () {

            }
        }
    }
</script>

<style scoped>

</style>