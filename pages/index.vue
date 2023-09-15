<template>
    <section>
        <div class="mainbig">
            <div class="main">


                <div class="main__body">
                    <h1>StudyNow.</h1>
                    <h2>Платформа для твоего развития</h2>

                    <div class="searchbody">
                        <div class="input-group">

                            <input type="text" class="form-control" placeholder="Поиск курса" aria-label="Username"
                                aria-describedby="basic-addon1" v-model="search" v-on:keyup.enter="redirectToCatalog">

                            <div class="input-group-prepend">
                                <NuxtLink :to="'/catalog?search=' + search">
                                    <span class="input-group-text" id="basic-addon1"><img src="@/assets/img/search.svg"
                                            alt="" loading="lazy"></span>
                                </NuxtLink>
                            </div>
                        </div>
                    </div>

                </div>


            </div>
        </div>

        <div class="page">
            <div class="sales">
                <a name="sales"></a>
                <h1>Акции и скидки</h1>

                <div class="sales__body">

                    <div class="sales__block" v-for="item in discounts" :key="item.id">
                        <img :src="pathUrl + '/api' + item.add_image[0]" class="productimg" />
                        <h2>{{ item.name }}</h2>
                        <p>{{ item.short_description }}</p>

                        <ul class="dot-list" v-if="item.key_features">
                            <li v-for="(feature, index) in item.key_features.split('\r\n').slice(0, 3)" :key="index">{{
                                                            feature }}
                            </li>
                        </ul>

                        <div class="price">
                            <span v-if="item.discount > 0">
                                {{ item.price.toLocaleString() + ' ₸' }}
                                <img src="@/assets/img/disc.svg" alt="" loading="lazy">
                            </span>
                            <h3 v-if="item.discount > 0">
                                {{ (Math.floor(item.price - ((item.price * item.discount) / 100))).toLocaleString() + ' ₸'
                                                                }}</h3>
                            <h3 v-else>{{ item.price == 0 ? 'Бесплатно' : item.price.toLocaleString() + ' ₸' }}</h3>
                        </div>

                        <div class="buttons">
                            <NuxtLink :to="'/product/' + item.id" ref="buy">
                                Подробнее
                            </NuxtLink>
                            <NuxtLink ref="buy" @click="addToCart(item.id)" style="cursor: pointer;">
                                {{ item.addToCartStatus || 'Купить' }}
                            </NuxtLink>
                        </div>
                    </div>

                </div>

                <div class="text-center link">
                    <NuxtLink to="/catalog">Посмотреть все</NuxtLink>
                </div>
            </div>

            <div class="category">
                <h1>Категории</h1>

                <div class="category__block">
                    <div>
                        <NuxtLink to="/catalog?category=1">
                            <span> IT</span>
                            <img src="@/assets/img/arrownt.svg" alt="" loading="lazy">
                        </NuxtLink>
                        <NuxtLink to="/catalog?category=2">
                            <span> Красота и здоровье</span>
                            <img src="@/assets/img/arrownt.svg" alt="" loading="lazy">
                        </NuxtLink>
                        <NuxtLink to="/catalog?category=3">
                            <span>Творчество и хобби</span>
                            <img src="@/assets/img/arrownt.svg" alt="" loading="lazy">
                        </NuxtLink>
                        <NuxtLink to="/catalog?category=4">
                            <span> Психология</span>
                            <img src="@/assets/img/arrownt.svg" alt="" loading="lazy">
                        </NuxtLink>

                    </div>
                    <div>
                        <NuxtLink to="/catalog?category=5">
                            <span> Духовное развитие</span>
                            <img src="@/assets/img/arrownt.svg" alt="" loading="lazy">
                        </NuxtLink>
                        <NuxtLink to="/catalog?category=6">
                            <span> Дети</span>
                            <img src="@/assets/img/arrownt.svg" alt="" loading="lazy">
                        </NuxtLink>
                        <NuxtLink to="/catalog?category=7">
                            <span>Маркетинг</span>
                            <img src="@/assets/img/arrownt.svg" alt="" loading="lazy">
                        </NuxtLink>
                        <NuxtLink to="/catalog?category=8">
                            <span>Финансы</span>
                            <img src="@/assets/img/arrownt.svg" alt="" loading="lazy">
                        </NuxtLink>

                    </div>

                    <div>
                        <NuxtLink to="/catalog?category=9">
                            <span> Радиотехника</span>
                            <img src="@/assets/img/arrownt.svg" alt="" loading="lazy">
                        </NuxtLink>
                        <NuxtLink to="/catalog?category=10">
                            <span> Бесплатные курсы</span>
                            <img src="@/assets/img/arrownt.svg" alt="" loading="lazy">
                        </NuxtLink>
                        <NuxtLink to="/catalog?category=11">
                            <span>Приготовление пищи</span>
                            <img src="@/assets/img/arrownt.svg" alt="" loading="lazy">
                        </NuxtLink>
                        <NuxtLink to="/catalog?category=12">
                            <span>Съёмка</span>
                            <img src="@/assets/img/arrownt.svg" alt="" loading="lazy">
                        </NuxtLink>

                    </div>

                    <div>
                        <NuxtLink to="/catalog?category=13">
                            <span> Языки</span>
                            <img src="@/assets/img/arrownt.svg" alt="" loading="lazy">
                        </NuxtLink>

                        <NuxtLink to="/catalog?category=14">
                            <span>Бизнес</span>
                            <img src="@/assets/img/arrownt.svg" alt="" loading="lazy">
                        </NuxtLink>

                        <NuxtLink to="/catalog?category=15">
                            <span>Спорт</span>
                            <img src="@/assets/img/arrownt.svg" alt="" loading="lazy">
                        </NuxtLink>

                    </div>

                    <div>
                        <NuxtLink to="/catalog?category=16">
                            <span> Разработка игр</span>
                            <img src="@/assets/img/arrownt.svg" alt="" loading="lazy">
                        </NuxtLink>

                        <NuxtLink to="/catalog?category=17">
                            <span>Продажи</span>
                            <img src="@/assets/img/arrownt.svg" alt="" loading="lazy">
                        </NuxtLink>

                        <NuxtLink to="/catalog?category=18">
                            <span>Мода</span>
                            <img src="@/assets/img/arrownt.svg" alt="" loading="lazy">
                        </NuxtLink>

                    </div>


                </div>
            </div>

            <div class="popular">
                <a name="popular"></a>
                <h1>Популярное</h1>

                <div class="sales__body">

                    <div class="sales__block" v-for="item in populars" :key="item.id">
                        <img :src="pathUrl + '/api' + item.add_image[0]" class="productimg" />
                        <h2>{{ item.name }}</h2>
                        <p>{{ item.short_description }}</p>

                        <ul class="dot-list" v-if="item.key_features">
                            <li v-for="(feature, index) in item.key_features.split('\r\n').slice(0, 3)" :key="index">{{
                                                            feature }}
                            </li>
                        </ul>

                        <div class="price">
                            <span v-if="item.discount > 0">
                                {{ item.price.toLocaleString() + ' ₸' }}
                                <img src="@/assets/img/disc.svg" alt="" loading="lazy">
                            </span>
                            <h3 v-if="item.discount > 0">
                                {{ (Math.floor(item.price - ((item.price * item.discount) / 100))).toLocaleString() + ' ₸'
                                                                }}</h3>
                            <h3 v-else>{{ item.price == 0 ? 'Бесплатно' : item.price.toLocaleString() + ' ₸' }}</h3>
                        </div>

                        <div class="buttons">
                            <NuxtLink :to="'/product/' + item.id" ref="buy">
                                Подробнее
                            </NuxtLink>
                            <NuxtLink ref="buy" @click="addToCart2(item.id)" style="cursor: pointer;">
                                {{ item.addToCartStatus || 'Купить' }}
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

                    <NuxtLink to="/about">Подробнее о платформе</NuxtLink>
                </div>
            </div>

            <div class="reviews">
                <h1>Отзывы</h1>

                <div class="review__slider">
                    <swiper :slides-per-view="3" :space-between="30" :breakpoints="breakpoints" :modules="modules"
                        :navigation="navigation">
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
                    <div class="pcnext">
                        <img src="@/assets/img/prev.svg" class="prev" alt="" loading="lazy">
                        <img src="@/assets/img/next.svg" class="next" alt="" loading="lazy">
                    </div>
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
import global from '~/mixins/global';
import axios from 'axios';
export default {
    mixins: [global],
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
                prevEl: '.prev',
                pathUrl: 'https://studynow.kz',
            },
            breakpoints: {
                320: {
                    slidesPerView: 1,
                    spaceBetween: 10,

                },
                1300: {
                    slidesPerView: 3,
                    spaceBetween: 30,
                }
            },
            discounts: [],
            populars: [],
            addToCartStatus: '',
        }
    },
    methods: {
        redirectToCatalog: function () {
            // Переход на '/catalog?search=' + this.search
            window.location.href = '/catalog?search=' + this.search;
        },
        addToCart(id) {
            const path = `${this.pathUrl}/api/buyer/add-product-basket`
            const csrf = this.getCSRFToken()
            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            axios
                .post(path, {
                    products: id,
                    amount: 1,
                })
                .then(response => {
                    const index = this.discounts.findIndex(item => item.id === id);
                    if (response.status == 201) {

                        this.discounts[index].addToCartStatus = 'Добавлен';
                    } else {
                        this.discounts[index].addToCartStatus = 'Ошибка';
                    }
                    console.log(response)
                })
                .catch(error => {
                    console.error(error)
                })
        },
        addToCart2(id) {
            const path = `${this.pathUrl}/api/buyer/add-product-basket`
            const csrf = this.getCSRFToken()
            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            axios
                .post(path, {
                    products: id,
                    amount: 1,
                })
                .then(response => {
                    const index = this.populars.findIndex(item => item.id === id);
                    if (response.status == 201) {
                        this.populars[index].addToCartStatus = 'Добавлен';
                    } else {
                        this.populars[index].addToCartStatus = 'Ошибка';
                    }
                    console.log(response)
                })
                .catch(error => {
                    console.error(error)
                })
        },
        getDiscount() {
            const path = `${this.pathUrl}/api/products/discount-product?amount_products=5`;
            axios
                .get(path)
                .then(response => {
                    this.discounts = response.data
                })
                .catch(error => {
                    console.log(error)
                })
        },
        getPopular() {
            const path = `${this.pathUrl}/api/products/popular-product?amount_products=5`;
            axios
                .get(path)
                .then(response => {
                    this.populars = response.data
                })
                .catch(error => {
                    console.log(error)
                })
        },
    },
    mounted() {
        this.getDiscount()
        this.getPopular()
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
.mouse {
    margin-top: 100px;

    @media (max-width: 1024px) {
        display: none !important;
    }


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

.productimg {
    height: 174px;
    width: 100%;
    object-fit: cover;
    border-radius: 10px;

    @media (max-width: 1024px) {
        height: 230px;
    }
}

.page {
    padding: 53px 110px 110px;

    @media (max-width: 1600px) {
        padding: 53px 50px 110px;
    }

    @media (max-width: 1024px) {
        padding: 30px 20px 50px;
    }

    .reviews {
        margin-top: 80px;

        @media (max-width: 1024px) {
            margin-top: 30px;
        }

        h1 {
            font-size: 40px;
            font-style: normal;
            font-weight: 500;
            line-height: 130%;
            font-family: var(--int);
            color: #000;

            @media (max-width: 1024px) {
                font-size: 24px;
            }
        }

        .review__slider {
            margin-top: 30px;
            display: flex;
            align-items: center;
            gap: 0 60px;

            @media (max-width: 1200px) {
                display: block;
                gap: 20px;
            }

            @media (max-width: 1024px) {
                margin-top: 15px;
            }


            .pcnext {
                display: flex;
                justify-content: center;
                margin-top: 20px;
                gap: 20px;

                .prev {
                    display: none;

                    @media(max-width: 1200px) {
                        display: block;
                    }
                }
            }

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

                    @media (max-width: 1024px) {
                        font-size: 16px;
                    }


                }

                p {
                    font-size: 16px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #000;
                    margin-bottom: 15px;

                    @media (max-width: 1024px) {
                        font-size: 12px;
                    }
                }

                span {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #000;

                    @media (max-width: 1024px) {
                        font-size: 16px;
                    }
                }
            }

            img {
                cursor: pointer;
            }
        }
    }

    .text__block {

        margin-top: 80px;

        @media (max-width: 1024px) {
            margin-top: 30px;
        }

        h2 {
            font-size: 40px;
            font-style: normal;
            font-weight: 400;
            line-height: 130%;
            font-family: var(--int);
            color: #000;

            padding: 0 218px;

            @media (max-width: 1600px) {
                padding: 0 150px;
            }

            @media (max-width: 1200px) {
                padding: 0;
                font-size: 30px;
            }

            @media (max-width: 1024px) {
                font-size: 18px;
                margin: 0;
            }
        }

        h1 {
            font-size: 40px;
            font-style: normal;
            font-weight: 400;
            line-height: 130%;
            font-family: var(--int);
            color: #000;
            margin-top: 30px;

            @media (max-width: 1024px) {
                font-size: 30px;
                margin-top: 20px;
            }

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

                @media (max-width: 1024px) {
                    font-size: 30px;
                }
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

            @media (max-width: 1024px) {
                margin-top: 20px;
            }

            &:hover {
                background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
            }
        }
    }

    .popular {
        margin-top: 80px;

        @media (max-width: 1024px) {
            margin-top: 30px;
        }

        h1 {
            font-size: 40px;
            font-style: normal;
            font-weight: 500;
            line-height: 130%;
            font-family: var(--int);
            color: #000;
            margin-bottom: 30px;

            @media (max-width: 1024px) {
                font-size: 24px;
            }
        }

        .sales__body {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            grid-auto-flow: dense;
            gap: 30px 50px;
            margin-top: 30px;


            @media (max-width: 1600px) {
                gap: 30px 40px;
            }

            @media (max-width: 1400px) {
                gap: 30px 20px;
                justify-content: center;
            }

            @media (max-width: 1024px) {
                margin-top: 15px;
                gap: 20px;
            }


            .sales__block {
                padding: 20px;
                border-radius: 10px;
                background: #fff;
                box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
                max-width: 100%;
                display: flex;
                flex-direction: column;

                @media (max-width: 1200px) {
                    max-width: 100%;
                    width: 100%;
                    padding: 10px;
                }


                h2 {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #000;
                    margin-top: 15px;
                    margin-bottom: 10px;

                    @media (max-width: 1024px) {
                        font-size: 16px;
                    }
                }

                p {
                    margin: 10px 0;
                    margin-top: auto !important;
                    font-size: 16px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 130%;
                    font-family: var(--int);

                    @media (max-width: 1024px) {
                        font-size: 12px;
                    }
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

                    @media (max-width: 1024px) {
                        font-size: 12px;
                    }
                }

                ul {
                    padding: 0;
                }

                .buttons {
                    display: flex;
                    margin-top: 10px;

                    gap: 10px;

                    @media (max-width: 1024px) {
                        padding: 0 20px;
                        flex-direction: row-reverse;
                    }

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

                    @media (max-width: 1024px) {
                        flex-direction: row-reverse;
                    }

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

                        @media (max-width: 1024px) {
                            font-size: 20px;
                        }
                    }
                }
            }
        }
    }

    .category {
        margin-top: 9px;

        @media (max-width: 1024px) {
            margin-top: 30px;
        }

        h1 {
            font-size: 40px;
            font-style: normal;
            font-weight: 500;
            line-height: 130%;
            font-family: var(--int);
            color: #000;
            margin-bottom: 30px;

            @media (max-width: 1024px) {
                font-size: 24px;
            }
        }

        .category__block {
            display: flex;
            flex-wrap: wrap;
            gap: 30px 80px;

            @media (max-width: 1200px) {
                flex-direction: column;
                flex-wrap: nowrap;
                gap: 20px;
            }

            div {
                display: flex;
                flex-direction: column;
                gap: 30px 0;

                @media (max-width: 1200px) {
                    gap: 20px;
                }
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

                @media (max-width: 1024px) {
                    font-size: 16px;
                }

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

            @media (max-width: 1024px) {
                font-size: 24px;
            }
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
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            grid-auto-flow: dense;
            margin-top: 30px;
            gap: 30px 50px;


            @media (max-width: 1600px) {
                gap: 30px 40px;
            }

            @media (max-width: 1400px) {
                gap: 30px 20px;
                justify-content: center;
            }

            @media (max-width: 1024px) {
                margin-top: 15px;
                gap: 20px;
            }


            .sales__block {
                padding: 20px;
                border-radius: 10px;
                background: #fff;
                box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
                max-width: 100%;
                display: flex;
                flex-direction: column;

                @media (max-width: 1200px) {
                    max-width: 100%;
                    width: 100%;
                    padding: 10px;
                }



                h2 {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #000;
                    margin-top: 15px;
                    margin-bottom: 10px;

                    @media (max-width: 1024px) {
                        font-size: 16px;
                    }
                }

                p {
                    margin: 10px 0;
                    margin-top: auto !important;
                    font-size: 16px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 130%;
                    font-family: var(--int);

                    @media (max-width: 1024px) {
                        font-size: 12px;
                    }
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

                    @media (max-width: 1024px) {
                        font-size: 12px;
                    }
                }

                ul {
                    padding: 0;
                }

                .buttons {
                    display: flex;
                    margin-top: 10px;

                    gap: 10px;

                    @media (max-width: 1024px) {
                        padding: 0 20px;
                        flex-direction: row-reverse;
                    }

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

                    @media (max-width: 1024px) {
                        flex-direction: row-reverse;

                        div {
                            display: none;
                        }
                    }

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

                        @media (max-width: 1024px) {
                            font-size: 20px;
                        }
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

    @media (max-width: 1024px) {
        background: url('@/assets/img/bgmob.png') no-repeat;
        background-size: 100%;
    }
}

.main {

    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;

    @media (max-width: 1024px) {
        height: auto;
        padding-top: 90px;
    }

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

            @media (max-width: 1200px) {
                font-size: 80px;
            }

            @media (max-width: 1024px) {
                font-size: 48px;
            }
        }

        h2 {
            font-size: 72px;
            font-style: normal;
            font-weight: 500;
            line-height: 120%;
            font-family: var(--int);
            color: #000;

            @media (max-width: 1200px) {
                font-size: 50px;
            }

            @media (max-width: 1024px) {
                font-size: 20px;
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

            @media (max-width: 1024px) {
                padding: 15px 20px;
            }

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
