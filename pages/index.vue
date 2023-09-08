<template>
    <section>
        <div class="main">

            <div class="main__body">
                <h1>StudyNow.</h1>
                <h2>Платформа для твоего развития</h2>

                <div class="searchbody">
                    <div class="input-group">

                        <input type="text" class="form-control" placeholder="Поиск курса" aria-label="Username"
                            aria-describedby="basic-addon1">

                        <div class="input-group-prepend">
                            <span class="input-group-text" id="basic-addon1"><img src="@/assets/img/search.svg"
                                    alt=""></span>
                        </div>
                    </div>
                </div>

                <div class="mouse">
                    <svg width="40" height="72" viewBox="0 0 40 72" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path
                            d="M19.9997 46.9997V41.9997M19.9997 68.6663C13.5564 68.6663 8.33301 63.443 8.33301 56.9997V46.9997C8.33301 40.5564 13.5564 35.333 19.9997 35.333C26.443 35.333 31.6663 40.5564 31.6663 46.9997V56.9997C31.6663 63.443 26.443 68.6663 19.9997 68.6663Z"
                            stroke="black" stroke-width="3" stroke-linecap="round" stroke-linejoin="round" />
                        <path d="M20 30L20 1" stroke="black" stroke-width="2" stroke-linecap="round" />
                        <circle cx="20" cy="8" r="4" fill="black" />
                    </svg>

                </div>
            </div>

        </div>

        <div class="page">
            <div class="sales">
                <h1>Акции и скидки</h1>

                <div class="sales__body">

                    <div class="sales__block">
                        <img src="@/assets/img/sales1.png" alt="">
                        <h2>Курсы визажиста «Make-up с нуля»</h2>
                        <p>Погрузись в мир красоты с курсом от профессионалов</p>

                        <ul class="dot-list">
                            <li>10 видеоуроков</li>
                            <li>3 эксперта</li>
                            <li>Быстрая обратная связь с разбором ошибок</li>
                        </ul>

                        <div class="price">
                            <span>
                                15 000 ₸
                                <img src="@/assets/img/disc.svg" alt="">
                            </span>
                            <h3>13 000 ₸</h3>
                            <div></div>
                        </div>

                        <div class="buttons">
                            <NuxtLink to="/">
                                Подробнее
                            </NuxtLink>
                            <NuxtLink to="/">
                                Купить
                            </NuxtLink>
                        </div>
                    </div>

                    <div class="sales__block">
                        <img src="@/assets/img/sales2.png" alt="">
                        <h2>«Сам себе кондитер»</h2>
                        <p>Начни зарабатывать, продавая домашнюю выпечку</p>

                        <ul class="dot-list">
                            <li>6 видеоуроков</li>
                            <li>Чек-лист для старта</li>
                            <li>Табличка с главными аллергенами</li>
                        </ul>

                        <div class="price">
                            <span>
                                20 000 ₸
                                <img src="@/assets/img/disc.svg" alt="">
                            </span>
                            <h3>15 000 ₸</h3>
                            <div></div>
                        </div>

                        <div class="buttons">
                            <NuxtLink to="/">
                                Подробнее
                            </NuxtLink>
                            <NuxtLink to="/">
                                Купить
                            </NuxtLink>
                        </div>
                    </div>

                    <div class="sales__block">
                        <img src="@/assets/img/sales3.png" alt="">
                        <h2>Современная профессия «Старт в smm»</h2>
                        <p>Комфортные условия для работы из дома</p>

                        <ul class="dot-list">
                            <li>16 лекций</li>
                            <li>Разбор работ</li>
                            <li>Список компаний для трудоустройства</li>
                        </ul>

                        <div class="price">
                            <span>
                                60 000 ₸
                                <img src="@/assets/img/disc.svg" alt="">
                            </span>
                            <h3>44 900 ₸</h3>
                            <div></div>
                        </div>

                        <div class="buttons">
                            <NuxtLink to="/">
                                Подробнее
                            </NuxtLink>
                            <NuxtLink to="/">
                                Купить
                            </NuxtLink>
                        </div>
                    </div>

                    <div class="sales__block">
                        <img src="@/assets/img/sales4.png" alt="">
                        <h2>«Гуру массажа»</h2>
                        <p>Экспертный курс для безопасного массажа</p>

                        <ul class="dot-list">
                            <li>9 видеоуроков</li>
                            <li>Схема с точками массажа</li>
                            <li>Лекции от медицинских работников</li>
                        </ul>

                        <div class="price">
                            <span>
                                14 000 ₸
                                <img src="@/assets/img/disc.svg" alt="">
                            </span>
                            <h3>11 000 ₸</h3>
                            <div></div>
                        </div>

                        <div class="buttons">
                            <NuxtLink to="/">
                                Подробнее
                            </NuxtLink>
                            <NuxtLink to="/">
                                Купить
                            </NuxtLink>
                        </div>
                    </div>

                    <div class="sales__block">
                        <img src="@/assets/img/sales5.png" alt="">
                        <h2>Курсы «Иллюстратор будущего»</h2>
                        <p>Рисунки на бумаге и графическом планшете</p>

                        <ul class="dot-list">
                            <li>15 видеоуроков</li>
                            <li>Разбор постоения рисунка</li>
                            <li>Книга по теории цвета</li>
                        </ul>

                        <div class="price">
                            <span>
                                37 000 ₸
                                <img src="@/assets/img/disc.svg" alt="">
                            </span>
                            <h3>27 000 ₸</h3>
                            <div></div>
                        </div>

                        <div class="buttons">
                            <NuxtLink to="/">
                                Подробнее
                            </NuxtLink>
                            <NuxtLink to="/">
                                Купить
                            </NuxtLink>
                        </div>
                    </div>

                </div>

                <div class="text-center link">
                    <NuxtLink to="/">Посмотреть все</NuxtLink>
                </div>
            </div>

            <div class="category">
                <h1>Категории</h1>

                <div class="category__block">
                    <div>
                        <NuxtLink to="/">
                            <span> IT</span>
                            <img src="@/assets/img/arrownt.svg" alt="">
                        </NuxtLink>
                        <NuxtLink to="/">
                            <span> Красота и здоровье</span>
                            <img src="@/assets/img/arrownt.svg" alt="">
                        </NuxtLink>
                        <NuxtLink to="/">
                            <span>Творчество и хобби</span>
                            <img src="@/assets/img/arrownt.svg" alt="">
                        </NuxtLink>
                        <NuxtLink to="/">
                            <span> Психология</span>
                            <img src="@/assets/img/arrownt.svg" alt="">
                        </NuxtLink>

                    </div>
                    <div>
                        <NuxtLink to="/">
                            <span> Духовное развитие</span>
                            <img src="@/assets/img/arrownt.svg" alt="">
                        </NuxtLink>
                        <NuxtLink to="/">
                            <span> Дети</span>
                            <img src="@/assets/img/arrownt.svg" alt="">
                        </NuxtLink>
                        <NuxtLink to="/">
                            <span>Маркетинг</span>
                            <img src="@/assets/img/arrownt.svg" alt="">
                        </NuxtLink>
                        <NuxtLink to="/">
                            <span>Финансы</span>
                            <img src="@/assets/img/arrownt.svg" alt="">
                        </NuxtLink>

                    </div>

                    <div>
                        <NuxtLink to="/">
                            <span> Радиотехника</span>
                            <img src="@/assets/img/arrownt.svg" alt="">
                        </NuxtLink>
                        <NuxtLink to="/">
                            <span> Бесплатные курсы</span>
                            <img src="@/assets/img/arrownt.svg" alt="">
                        </NuxtLink>
                        <NuxtLink to="/">
                            <span>Приготовление пищи</span>
                            <img src="@/assets/img/arrownt.svg" alt="">
                        </NuxtLink>
                        <NuxtLink to="/">
                            <span>Съёмка</span>
                            <img src="@/assets/img/arrownt.svg" alt="">
                        </NuxtLink>

                    </div>

                    <div>
                        <NuxtLink to="/">
                            <span> Языки</span>
                            <img src="@/assets/img/arrownt.svg" alt="">
                        </NuxtLink>

                        <NuxtLink to="/">
                            <span>Бизнес</span>
                            <img src="@/assets/img/arrownt.svg" alt="">
                        </NuxtLink>

                        <NuxtLink to="/">
                            <span>Спорт</span>
                            <img src="@/assets/img/arrownt.svg" alt="">
                        </NuxtLink>

                    </div>

                    <div>
                        <NuxtLink to="/">
                            <span> Разработка игр</span>
                            <img src="@/assets/img/arrownt.svg" alt="">
                        </NuxtLink>

                        <NuxtLink to="/">
                            <span>Продажи</span>
                            <img src="@/assets/img/arrownt.svg" alt="">
                        </NuxtLink>

                        <NuxtLink to="/">
                            <span>Мода</span>
                            <img src="@/assets/img/arrownt.svg" alt="">
                        </NuxtLink>

                    </div>


                </div>
            </div>

            <div class="popular">
                <h1>Популярное</h1>

                <div class="sales__body">

                    <div class="sales__block">
                        <img src="@/assets/img/sales1.png" alt="">
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
                            <NuxtLink to="/">
                                Подробнее
                            </NuxtLink>
                            <NuxtLink to="/">
                                Купить
                            </NuxtLink>
                        </div>
                    </div>

                    <div class="sales__block">
                        <img src="@/assets/img/sales2.png" alt="">
                        <h2>«Сам себе кондитер»</h2>
                        <p>Начни зарабатывать, продавая домашнюю выпечку</p>

                        <ul class="dot-list">
                            <li>6 видеоуроков</li>
                            <li>Чек-лист для старта</li>
                            <li>Табличка с главными аллергенами</li>
                        </ul>

                        <div class="price">

                            <h3>15 000 ₸</h3>
                        </div>

                        <div class="buttons">
                            <NuxtLink to="/">
                                Подробнее
                            </NuxtLink>
                            <NuxtLink to="/">
                                Купить
                            </NuxtLink>
                        </div>
                    </div>

                    <div class="sales__block">
                        <img src="@/assets/img/sales3.png" alt="">
                        <h2>Современная профессия «Старт в smm»</h2>
                        <p>Комфортные условия для работы из дома</p>

                        <ul class="dot-list">
                            <li>16 лекций</li>
                            <li>Разбор работ</li>
                            <li>Список компаний для трудоустройства</li>
                        </ul>

                        <div class="price">

                            <h3>44 900 ₸</h3>
                        </div>

                        <div class="buttons">
                            <NuxtLink to="/">
                                Подробнее
                            </NuxtLink>
                            <NuxtLink to="/">
                                Купить
                            </NuxtLink>
                        </div>
                    </div>

                    <div class="sales__block">
                        <img src="@/assets/img/sales4.png" alt="">
                        <h2>«Гуру массажа»</h2>
                        <p>Экспертный курс для безопасного массажа</p>

                        <ul class="dot-list">
                            <li>9 видеоуроков</li>
                            <li>Схема с точками массажа</li>
                            <li>Лекции от медицинских работников</li>
                        </ul>

                        <div class="price">

                            <h3>11 000 ₸</h3>
                        </div>

                        <div class="buttons">
                            <NuxtLink to="/">
                                Подробнее
                            </NuxtLink>
                            <NuxtLink to="/">
                                Купить
                            </NuxtLink>
                        </div>
                    </div>

                    <div class="sales__block">
                        <img src="@/assets/img/sales5.png" alt="">
                        <h2>Курсы «Иллюстратор будущего»</h2>
                        <p>Рисунки на бумаге и графическом планшете</p>

                        <ul class="dot-list">
                            <li>15 видеоуроков</li>
                            <li>Разбор постоения рисунка</li>
                            <li>Книга по теории цвета</li>
                        </ul>

                        <div class="price">
                            <h3>27 000 ₸</h3>
                        </div>

                        <div class="buttons">
                            <NuxtLink to="/">
                                Подробнее
                            </NuxtLink>
                            <NuxtLink to="/">
                                Купить
                            </NuxtLink>
                        </div>
                    </div>

                </div>
            </div>

            <div class="text__block">
                <div class="text-right">
                    <h2> Виртуальное образовательное пространство</h2>
                </div>
                <div class="text-left">
                    <h2>предоставляет гибкость обучения, интерактивные материалы,
                        видеолекции, тексты и практические задания для всех пользователей</h2>
                </div>
                <div class="text-center">
                    <h1>Попробуйте <span>StudyNow</span></h1>

                    <NuxtLink to="/">Подробнее о платформе</NuxtLink>
                </div>
            </div>

            <div class="reviews">
                <h1>Отзывы</h1>

                <div class="review__slider">
                    <swiper :slides-per-view="3" :space-between="30" :modules="modules" :navigation="navigation">
                        <swiper-slide class="slide">
                            <h2>Все лучшие преподаватели здесь</h2>
                            <p class="mb-0">
                                Эта платформа стала для меня настоящим открытием! Здесь так много разнообразных курсов на
                                самые разные темы. Я начала с курса по фотографии и была поражена качеством материалов и
                                профессионализмом инструкторов.
                            </p>
                            <div class="text-right">
                                <span>Дарья</span>
                            </div>
                        </swiper-slide>

                        <swiper-slide class="slide">
                            <h2>Все лучшие преподаватели здесь</h2>
                            <p class="mb-0">
                                Эта платформа стала для меня настоящим открытием! Здесь так много разнообразных курсов на
                                самые разные темы. Я начала с курса по фотографии и была поражена качеством материалов и
                                профессионализмом инструкторов.
                            </p>
                            <div class="text-right">
                                <span>Дарья</span>
                            </div>
                        </swiper-slide>

                        <swiper-slide class="slide">
                            <h2>Все лучшие преподаватели здесь</h2>
                            <p class="mb-0">
                                Эта платформа стала для меня настоящим открытием! Здесь так много разнообразных курсов на
                                самые разные темы. Я начала с курса по фотографии и была поражена качеством материалов и
                                профессионализмом инструкторов.
                            </p>
                            <div class="text-right">
                                <span>Дарья</span>
                            </div>
                        </swiper-slide>

                        <swiper-slide class="slide">
                            <h2>Все лучшие преподаватели здесь</h2>
                            <p class="mb-0">
                                Эта платформа стала для меня настоящим открытием! Здесь так много разнообразных курсов на
                                самые разные темы. Я начала с курса по фотографии и была поражена качеством материалов и
                                профессионализмом инструкторов.
                            </p>
                            <div class="text-right">
                                <span>Дарья</span>
                            </div>
                        </swiper-slide>


                    </swiper>

                    <img src="@/assets/img/next.svg" class="next" alt="">
                </div>
            </div>
        </div>
    </section>
</template>
<script>
// Import Swiper Vue.js components
import { Navigation } from 'swiper/modules';
import { Swiper, SwiperSlide } from 'swiper/vue';

// Import Swiper styles
import 'swiper/css';
export default {
    components: {
        Swiper,
        SwiperSlide,
    },
    data() {
        return {
            search: '',
            modules: [Navigation],
            navigation: {
                nextEl: '.next',
            },
        }
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Главная | Studynow',
    ogTitle: 'Главная | Studynow',
    description: 'Главная | Studynow',
    ogDescription: 'Главная | Studynow',
})
</script>
<style lang="scss" scoped>
.page {
    padding: 53px 110px 110px;

    .reviews {
        margin-top: 80px;

        h1 {
            font-size: 40px;
            font-style: normal;
            font-weight: 500;
            line-height: 130%;
            font-family: var(--int);
            color: #000;
        }

        .review__slider {
            margin-top: 30px;
            display: flex;
            align-items: center;
            gap: 0 60px;

            .slide {
                padding: 20px;
                border-radius: 15px;
                background: #FFF;
                box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
                max-width: 500px;

                h2 {
                    background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
                    background-clip: text;
                    -webkit-background-clip: text;
                    -webkit-text-fill-color: transparent;

                    font-size: 20px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: 130%;
                    font-family: var(--int);
                    margin-bottom: 15px;


                }

                p {
                    font-size: 16px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #000;
                    margin-bottom: 15px;
                }

                span {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #000;
                }
            }

            img {
                cursor: pointer;
            }
        }
    }

    .text__block {

        margin-top: 80px;

        h2 {
            font-size: 40px;
            font-style: normal;
            font-weight: 400;
            line-height: 130%;
            font-family: var(--int);
            color: #000;

            padding: 0 218px;
        }

        h1 {
            font-size: 40px;
            font-style: normal;
            font-weight: 400;
            line-height: 130%;
            font-family: var(--int);
            color: #000;
            margin-top: 30px;

            span {
                background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
                background-clip: text;
                -webkit-background-clip: text;
                -webkit-text-fill-color: transparent;
                font-family: var(--int);
                font-size: 40px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
            }
        }

        a {
            padding: 10px 30px;
            border-radius: 10px;
            background: #000;
            border: 0;
            text-decoration: none;
            margin-top: 30px;
            display: inline-block;

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

    .popular {
        margin-top: 80px;

        h1 {
            font-size: 40px;
            font-style: normal;
            font-weight: 500;
            line-height: 130%;
            font-family: var(--int);
            color: #000;
            margin-bottom: 30px;
        }

        .sales__body {
            display: flex;
            flex-wrap: wrap;
            margin-top: 30px;
            gap: 30px 50px;

            .sales__block {
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

    .category {
        margin-top: 9px;

        h1 {
            font-size: 40px;
            font-style: normal;
            font-weight: 500;
            line-height: 130%;
            font-family: var(--int);
            color: #000;
            margin-bottom: 30px;
        }

        .category__block {
            display: flex;
            flex-wrap: wrap;
            gap: 30px 80px;

            div {
                display: flex;
                flex-direction: column;
                gap: 30px 0;
            }

            a {
                text-decoration: none;
                font-size: 24px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
                transition: background 0.3s ease, color 0.3s ease;

                display: flex;
                align-items: center;
                gap: 0 10px;

                img {
                    display: block;
                    transition: opacity 0.3s ease;
                }

                &:hover {
                    background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
                    background-clip: text;
                    -webkit-background-clip: text;
                    -webkit-text-fill-color: transparent;
                }

                &:hover img {
                    opacity: 0;
                }


            }
        }
    }

    .sales {
        h1 {
            font-size: 40px;
            font-style: normal;
            font-weight: 500;
            line-height: 130%;
            font-family: var(--int);
            color: #000;
            margin-bottom: 0;
        }

        .link {
            margin-top: 30px;

            a {
                border-radius: 10px;
                background: #000;
                padding: 10px 30px;
                text-align: center;
                text-decoration: none;

                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                color: #fff;
                font-family: var(--int);

                transition: all .3s ease;

                &:hover {
                    background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
                }
            }
        }

        .sales__body {
            display: flex;
            flex-wrap: wrap;
            margin-top: 30px;
            gap: 30px 50px;

            .sales__block {
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
}

section {
    background: url('@/assets/img/bgmain.png');
    background-repeat: no-repeat;
    background-position: top;
}

.main {

    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;




    .main__body {
        h1 {
            font-size: 128px;
            font-style: normal;
            font-weight: 500;
            line-height: 130%;
            font-family: var(--int);
            background: linear-gradient(90deg, #462885 0.64%, #A021A7 52.97%);
            background-clip: text;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        h2 {
            font-size: 72px;
            font-style: normal;
            font-weight: 500;
            line-height: 120%;
            font-family: var(--int);
            color: #000;
        }

        .mouse {
            margin-top: 150px;


            @keyframes scaleAnimation {
                0% {
                    transform: scale(1);
                }

                50% {
                    transform: scale(1.2);
                    /* Увеличение до 1.2x исходного размера */
                }

                100% {
                    transform: scale(1);
                }
            }


            svg {
                cursor: pointer;
                animation: scaleAnimation 2s infinite;
                /* 3s - продолжительность анимации, infinite - бесконечное повторение */
                transform-origin: center;
                /* Центральная точка масштабирования */
            }
        }

        .searchbody {
            border-radius: 15px;
            background: rgba(244, 244, 244, 0.70);
            box-shadow: -38.66667px 38.66667px 38.66667px 0px rgba(255, 255, 255, 0.20) inset, 38.66667px -38.66667px 38.66667px 0px rgba(192, 182, 194, 0.20) inset;
            backdrop-filter: blur(38.66666793823242px);
            padding: 15px 40px;
            text-align: center;
            margin: 52px 20px 0;

            input {
                border-radius: 10px;
                background: #FFF;
                padding: 12px 30px;
                font-family: var(--int);
                color: #3C3C3C;
                border: 0;
                height: 50px;
                border-top-right-radius: 0;
                border-bottom-right-radius: 0;
                box-shadow: none !important;
            }


            .input-group-text {
                background: #fff;
                border-radius: 10px;
                border-top-left-radius: 0;
                border-bottom-left-radius: 0;
                border: 0;
                height: 50px;
            }
        }
    }
}
</style>
