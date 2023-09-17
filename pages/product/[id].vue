<template>
    <div class="product">

        <prevPage />
        <div v-if="product.length <= 0"></div>
        <div class="product__body" v-else>
            <h1>{{ product.name }}</h1>


            <div class="images__slider">
                <swiper :slides-per-view="2" :space-between="20" :modules="modules" :navigation="navigation">
                    <swiper-slide class="slide" v-for="img in product.add_image" :key="img.id">
                        <div class="slide-content">
                            <img :src="img.image" alt="" width="165" height="110">
                        </div>
                    </swiper-slide>
                    <img src="@/assets/img/next.svg" class="next" alt="" loading="lazy">
                </swiper>

            </div>
            <div class="product__info">
                <div class="product__images">
                    <img v-for="img in product.add_image" :src="img.image" alt="" loading="lazy">
                    <!-- <img src="@/assets/img/product2.png" alt="" loading="lazy">
                    <img src="@/assets/img/product3.png" alt="" loading="lazy"> -->
                </div>
                <div class="w-100">

                    <div class="product__full">
                        <div class="product__about">
                            <span>Категория курса:</span> <small>{{ product.category.category_name }}</small>
                            <h2>{{ product.short_description }}</h2>

                            <ul class="dot-list">
                                <li v-for="(feature, index) in product.key_features.split('\r\n')" :key="index">{{ feature
                                }}
                                </li>

                            </ul>

                            <div class="price">
                                <div>
                                    <small v-if="product.discount > 0">{{ product.price.toLocaleString() + ' ₸' }}
                                        <img src="@/assets/img/disc.svg" alt="" loading="lazy"> </small>
                                    <h3 v-if="product.discount > 0">
                                        {{ (Math.floor(product.price - ((product.price * product.discount) /
                                            100))).toLocaleString() + ' ₸' }}
                                    </h3>
                                    <h3 v-else>
                                        {{ product.price == 0 ? 'Бесплатно' : product.price.toLocaleString() + ' ₸' }}
                                    </h3>
                                </div>
                                <button class="mb-1" ref="cartBtn" @click="addToCart()">Купить</button>
                            </div>
                        </div>
                        <div class="product__seller">
                            <div>
                                <span>Автор:</span>
                                <small>{{ seller.first_name }}</small>
                            </div>
                            <div>
                                <span>Рейтинг:</span>
                                <the-rating :rating="rating"></the-rating>
                            </div>
                            <div>
                                <span>Курсов на платформе:</span>
                                <small>{{ count }}</small>
                            </div>

                            <div class="justify-content-center">
                                <NuxtLink :to="'/author/' + product.seller.id">Профиль продавца</NuxtLink>
                            </div>
                        </div>
                    </div>


                    <div class="product__desc">
                        <div v-html="product.description"></div>
                    </div>
                </div>

                <div class="sellermob">
                    <div class="product__seller sellermob2">
                        <div>
                            <span>Автор:</span>
                            <small>{{ seller.first_name }}</small>
                        </div>
                        <div>
                            <span>Рейтинг:</span>
                            <the-rating :rating="rating"></the-rating>
                        </div>
                        <div>
                            <span>Курсов на платформе:</span>
                            <small>{{ count }}</small>
                        </div>

                        <div class="justify-content-center">
                            <NuxtLink :to="'/author/' + product.seller.id">Профиль продавца</NuxtLink>
                        </div>
                    </div>
                </div>
            </div>

        </div>
    </div>
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
    data() {
        return {
            productId: this.$route.params.id,
            product: [],
            seller: [],
            pathUrl: 'https://studynow.kz',
            category: '',
            rating: null,
            count: null,
            modules: [Navigation],
            navigation: {
                nextEl: '.next',
            },
        }
    },
    components: {
        Swiper,
        SwiperSlide,

    },
    methods: {
        addToCart() {
            const path = `${this.pathUrl}/api/buyer/add-product-basket`
            const csrf = this.getCSRFToken()
            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            axios
                .post(path, {
                    products: this.product.id,
                    amount: 1,
                })
                .then(response => {
                    if (response.status == 201) {
                        this.$refs.cartBtn.innerHTML = 'Добавлен'
                        this.$refs.cartBtn.disabled = true
                        this.$refs.cartBtn.classList.add('disabled')
                    }
                    else {
                        this.$refs.cartBtn.innerHTML = 'Ошибка'
                        this.$refs.cartBtn.disabled = false

                    }
                    console.log(response)
                })
                .catch(error => {
                    console.error(error)
                })
        },
        getProduct() {
            const path = `${this.pathUrl}/api/products/detail-product/${this.productId}`
            axios
                .get(path)
                .then(response => {
                    this.product = response.data
                    this.seller = response.data.seller.user
                    this.rating = response.data.seller.rating
                    this.category = response.data.category.category_name
                    this.count = response.data.seller.amount_products
                })
                .catch(error => {
                    console.error(error)
                })
        },
    },
    mounted() {
        this.getProduct()
    }


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
.images__slider {
    display: none;
    overflow: hidden;

    .slide {
        position: relative;
    }

    .next {
        position: absolute;
        right: 0;
        top: 20%;
        z-index: 20;
    }

    .swiper-slide {}

    @media (max-width: 500px) {
        display: flex;
    }

    // img {
    //     width: 165px;
    //     height: 110px;
    // }
}

.product {
    padding: 120px 110px 55px;

    @media (max-width: 1600px) {
        padding: 120px 50px 55px;
    }

    @media (max-width: 1200px) {
        padding: 120px 20px 55px;
    }

    .product__body {
        .product__info {
            display: flex;
            align-items: start;
            gap: 50px;


            @media (max-width: 1200px) {
                flex-direction: column;
                gap: 20px;
            }

            .product__desc {
                margin-top: 39px;

                @media (max-width: 1200px) {
                    margin-top: 20px;
                }

                div {
                    font-family: var(--int);
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 130%;
                    color: #000;
                    max-width: 1095px;
                    white-space: break-spaces;

                    @media (max-width: 1200px) {
                        font-size: 16px;
                        max-width: auto;
                        overflow: hidden;
                    }

                    @media (max-width: 420px) {
                        font-size: 16px;
                        max-width: 350px;
                    }
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

                    @media (max-width: 1200px) {
                        display: none;
                    }

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

                        @media (max-width: 1200px) {
                            font-size: 16px;
                        }
                    }

                    small {
                        font-size: 20px;
                        font-style: normal;
                        font-weight: 400;
                        line-height: 130%;
                        font-family: var(--int);
                        color: #000;

                        @media (max-width: 1200px) {
                            font-size: 16px;
                        }
                    }

                    h2 {
                        font-size: 20px;
                        font-style: normal;
                        font-weight: 400;
                        line-height: 130%;
                        font-family: var(--int);
                        color: #000;
                        margin-top: 30px;

                        @media (max-width: 1200px) {
                            font-size: 16px;
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

                        @media (max-width: 1200px) {
                            font-size: 14px;
                        }
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
                        align-items: flex-end;
                        gap: 40px;

                        @media (max-width: 1200px) {
                            align-items: center;
                        }

                        small {
                            position: relative;
                            font-size: 16px;
                            font-style: normal;
                            font-weight: 400;
                            line-height: 130%;
                            font-family: var(--int);
                            color: #000;

                            @media (max-width: 1200px) {
                                font-size: 14px;
                            }

                            img {
                                position: absolute;
                                left: 0;
                                bottom: 5%;
                            }

                        }

                        h3 {
                            font-size: 40px;
                            font-style: normal;
                            font-weight: 500;
                            line-height: 130%;
                            font-family: var(--int);
                            color: #000;
                            margin-bottom: 0;

                            @media (max-width: 1200px) {
                                font-size: 16px;
                            }
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

                @media (max-width: 1200px) {
                    justify-content: flex-start;
                    flex-direction: row;
                    flex-wrap: wrap;
                    gap: 20px;
                }

                @media (max-width: 500px) {
                    display: none;
                }

                @media (max-width: 389px) {
                    justify-content: center;
                }

                img {
                    width: 469.997px;
                    height: 321.005px;

                    @media (max-width: 1400px) {
                        width: 420px;
                        width: 320px;

                    }

                    @media (max-width: 1200px) {
                        width: 45%;
                        height: auto;
                    }

                    @media (max-width: 1024px) {
                        width: 100%;
                        height: auto;
                    }
                }
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

            @media (max-width: 1200px) {
                font-size: 24px;
                margin-bottom: 20px;
            }
        }
    }

}

.sellermob {
    display: none;

    @media (max-width: 1024px) {
        display: block;
        width: 100%;
    }

    .product__seller {
        border-radius: 10px;
        background: #fff;
        box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
        padding: 30px 20px;
        width: 100%;

        @media (max-width: 1024px) {
            padding: 15px;
        }

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
                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
            }

            small {
                font-size: 16px;
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
}
</style>