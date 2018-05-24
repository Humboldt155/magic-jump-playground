<template>
    <section>
        <nav class="navbar is-transparent">
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
    </section>
</template>

<script>

    import axios from 'axios';

    export default {
        name: "code_projects"
    }
</script>

<style scoped>

</style>