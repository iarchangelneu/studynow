<template>
    <div class="product">

        <prevPage />

        <div class="product__body">
            <h1>Курс «Блюда высокой кухни со всех стран»</h1>



            <div class="product__info">
                <div class="product__images">
                    <img src="@/assets/img/product1.png" alt="" loading="lazy">
                    <img src="@/assets/img/product2.png" alt="" loading="lazy">
                    <img src="@/assets/img/product3.png" alt="" loading="lazy">
                </div>


                <div class="w-100">

                    <div class="product__full">
                        <div class="product__about">
                            <span>Категория курса:</span> <small>Приготовление пищи</small>
                            <h2>Сборник лучших рецептов кухонь Мира</h2>

                            <ul class="dot-list">
                                <li>10 видеоуроков</li>
                                <li>3 эксперта</li>
                                <li>Быстрая обратная связь с разбором ошибок</li>
                                <li>Что</li>
                                <li>Ты</li>
                                <li>Сосешь?</li>
                            </ul>

                            <div class="price">
                                <h3>
                                    50 490 ₸
                                </h3>
                                <button>Купить</button>
                            </div>
                        </div>
                        <div class="product__seller">
                            <div>
                                <span>Автор:</span>
                                <small>Анна Скобина</small>
                            </div>
                            <div>
                                <span>Рейтинг:</span>
                                <the-rating :rating="5"></the-rating>
                            </div>
                            <div>
                                <span>Курсов на платформе:</span>
                                <small>1</small>
                            </div>

                            <div class="justify-content-center">
                                <NuxtLink to="/">Профиль продавца</NuxtLink>
                            </div>
                        </div>
                    </div>


                    <div class="product__desc">
                        <div v-html="text"></div>
                    </div>
                </div>

            </div>

        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            text: 'Тест описания <br> Тест описания <br>Тест описания <br>Тест описания <br> Тест описания <br>Тест описания <br>Тест описания <br> Тест описания <br>Тест описания <br>'
        }
    },
    methods: {
        goBack() {
            this.prevPage = this.$nuxt.$router.go(-1); // Вернуться на предыдущий маршрут
        },
    },


}
</script>
<script setup>
useSeoMeta({
    title: 'Страница товара | Studynow',
    ogTitle: 'Страница товара | Studynow',
    description: 'Страница товара | Studynow',
    ogDescription: 'Страница товара | Studynow',
})
</script>
<style lang="scss" scoped>
.product {
    padding: 120px 110px 55px;

    .product__body {
        .product__info {
            display: flex;
            align-items: start;
            gap: 50px;

            .product__desc {
                margin-top: 39px;

                div {
                    font-family: var(--int);
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 130%;
                    color: #000;
                }
            }

            .product__full {
                width: 100%;
                display: flex;
                align-items: flex-start;
                justify-content: space-between;

                .product__seller {
                    border-radius: 10px;
                    background: #fff;
                    box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
                    padding: 30px 20px;
                    width: 24.896vw;

                    a {
                        text-decoration: none;
                        text-align: center;
                        padding: 10px 30px;
                        display: inline-block;
                        margin-top: 5px;
                        border-radius: 10px;
                        background: #000;

                        font-size: 16px;
                        font-style: normal;
                        font-weight: 400;
                        line-height: 130%;
                        font-family: var(--int);
                        color: #fff;

                        &:hover {
                            background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
                        }
                    }

                    div {
                        display: flex;
                        justify-content: space-between;
                        align-items: center;
                        margin-bottom: 20px;

                        span {
                            font-size: 20px;
                            font-style: normal;
                            font-weight: 400;
                            line-height: 130%;
                            font-family: var(--int);
                            color: #000;
                        }

                        small {
                            font-size: 20px;
                            font-style: normal;
                            font-weight: 500;
                            line-height: 130%;
                            font-family: var(--int);
                            color: #000;
                        }

                        &:last-child {
                            margin-bottom: 0;
                        }
                    }
                }

                .product__about {
                    span {
                        font-size: 20px;
                        font-style: normal;
                        font-weight: 600;
                        line-height: 130%;
                        font-family: var(--int);
                        color: #000;
                    }

                    small {
                        font-size: 20px;
                        font-style: normal;
                        font-weight: 400;
                        line-height: 130%;
                        font-family: var(--int);
                        color: #000;
                    }

                    h2 {
                        font-size: 20px;
                        font-style: normal;
                        font-weight: 400;
                        line-height: 130%;
                        font-family: var(--int);
                        color: #000;
                        margin-top: 30px;
                    }

                    li {
                        font-size: 16px;
                        font-style: normal;
                        font-weight: 400;
                        line-height: 130%;
                        font-family: var(--int);
                        color: #3C3C3C;
                        margin-bottom: 10px;
                        position: relative;
                        display: flex;
                        align-items: flex-start;
                        white-space: normal;
                    }

                    .dot-list {
                        list-style-type: none;
                        margin-top: 30px;
                        padding: 0;

                        li::before {
                            content: "";
                            min-width: 10px;
                            min-height: 10px;
                            background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
                            border-radius: 50%;
                            margin-right: 15px;
                            margin-top: 5px;
                        }

                    }

                    .price {
                        display: flex;
                        align-items: center;
                        gap: 40px;

                        h3 {
                            font-size: 40px;
                            font-style: normal;
                            font-weight: 500;
                            line-height: 130%;
                            font-family: var(--int);
                            color: #000;
                            margin-bottom: 0;
                        }

                        button {
                            padding: 10px 30px;
                            border: 0;
                            border-radius: 10px;
                            background: #000;

                            font-size: 16px;
                            font-style: normal;
                            font-weight: 400;
                            line-height: 130%;
                            font-family: var(--int);
                            color: #fff;

                            &:hover {
                                background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
                            }
                        }
                    }
                }
            }

            .product__images {
                display: flex;
                flex-direction: column;
                gap: 50px;
            }
        }

        margin-top: 10px;


        h1 {
            font-size: 40px;
            font-style: normal;
            font-weight: 500;
            line-height: 130%;
            font-family: var(--int);
            color: #000;
            margin-bottom: 30px;
        }
    }

}
</style>