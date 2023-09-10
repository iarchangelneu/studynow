<template>
    <div class="author">

        <prevPage />

        <h1>Анна Скобина</h1>


        <div class="author__desc">
            <img src="@/assets/img/avatar.png" alt="" loading="lazy">

            <div>
                <div v-html="description"></div>
            </div>
        </div>


        <div class="author__products">
            <h1>Курсы автора</h1>

            <div class="author__items">
                <div class="author__item">
                    <img src="@/assets/img/sales1.png" />
                    <h2>Курсы визажиста «Make-up с нуля»</h2>
                    <p>Погрузись в мир красоты с курсом от профессионалов</p>

                    <ul class="dot-list">
                        <li>10 видеоуроков</li>
                        <li>3 эксперта</li>
                        <li>Быстрая обратная связь с разбором ошибок</li>
                    </ul>

                    <div class="price">
                        <h3>13 000 ₸</h3>
                    </div>

                    <div class="buttons">
                        <NuxtLink to="/product">
                            Подробнее
                        </NuxtLink>
                        <NuxtLink to="/">
                            Купить
                        </NuxtLink>
                    </div>
                </div>
                <div class="author__item">
                    <img src="@/assets/img/sales1.png" />
                    <h2>Курсы визажиста «Make-up с нуля»</h2>
                    <p>Погрузись в мир красоты с курсом от профессионалов</p>

                    <ul class="dot-list">
                        <li>10 видеоуроков</li>
                        <li>3 эксперта</li>
                        <li>Быстрая обратная связь с разбором ошибок</li>
                    </ul>

                    <div class="price">
                        <h3>13 000 ₸</h3>
                    </div>

                    <div class="buttons">
                        <NuxtLink to="/product">
                            Подробнее
                        </NuxtLink>
                        <NuxtLink to="/">
                            Купить
                        </NuxtLink>
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
            description: 'Меня зовут Анна, и я — путешественница по миру знаний и навыков. Здесь я рада делиться с вами моими увлекательными и разнообразными курсами. Я верю в бесконечные возможности саморазвития и в то, что каждый из нас может стать лучше, осваивая новые области.'
        }
    },
    methods: {
        methods: {
            goBack() {
                this.prevPage = this.$nuxt.$router.go(-1); // Вернуться на предыдущий маршрут
            },
        },
    }
}
</script >
<script setup>
useSeoMeta({
    title: 'Страница автора | Studynow',
    ogTitle: 'Страница автора | Studynow',
    description: 'Страница автора | Studynow',
    ogDescription: 'Страница автора | Studynow',
})
</script>
<style lang="scss" scoped>
.author {
    padding: 120px 110px 110px;


    .author__products {
        margin-top: 50px;

        h1 {
            font-size: 40px;
            font-style: normal;
            font-weight: 500;
            line-height: 130%;
            font-family: var(--int);
            color: #000;
            margin-top: 10px;
            margin-bottom: 30px;
        }

        .author__items {
            display: flex;
            flex-wrap: wrap;
            gap: 50px;

            .author__item {
                padding: 20px;
                border-radius: 10px;
                background: #fff;
                box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
                max-width: 300px;
                display: flex;
                flex-direction: column;

                h2 {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #000;
                    margin-top: 15px;
                    margin-bottom: 10px;
                }

                p {
                    margin: 10px 0;
                    margin-top: auto !important;
                    font-size: 16px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 130%;
                    font-family: var(--int);
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

                ul {
                    padding: 0;
                }

                .buttons {
                    display: flex;
                    margin-top: 10px;

                    gap: 10px;

                    a {
                        padding: 10px 15px;
                        text-align: center;
                        background: #000;
                        border-radius: 10px;
                        border: 0;
                        flex: 1;
                        text-decoration: none;

                        font-size: 16px;
                        font-style: normal;
                        font-weight: 400;
                        line-height: 130%;
                        font-family: var(--int);
                        color: #fff;
                        transition: all .3s ease;

                        &:hover {
                            background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
                        }
                    }
                }

                .dot-list {
                    list-style-type: none;

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
                    justify-content: center;
                    gap: 0 28px;

                    span {
                        font-size: 12px;
                        font-style: normal;
                        font-weight: 400;
                        line-height: 130%;
                        font-family: var(--int);
                        color: #000;
                        position: relative;

                        img {
                            position: absolute;
                            left: 0;
                        }
                    }

                    h3 {
                        font-size: 24px;
                        font-style: normal;
                        font-weight: 500;
                        line-height: 130%;
                        font-family: var(--int);
                        color: #000;
                    }
                }
            }
        }
    }

    .author__desc {
        margin-top: 30px;
        display: flex;
        gap: 30px;
    }

    h1 {
        font-size: 40px;
        font-style: normal;
        font-weight: 500;
        line-height: 130%;
        font-family: var(--int);
        color: #000;
        margin-top: 10px;
        margin-bottom: 0;
    }


}
</style>