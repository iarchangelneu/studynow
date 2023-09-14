<template>
    <div class="author">

        <prevPage />

        <h1 v-if="author.user">{{ author.user.first_name }}</h1>


        <div class="author__desc">
            <div class="avatar">
                <img :src="author.photo" alt="" loading="lazy">
            </div>

            <div v-if="author.description">
                <div v-html="author.description" class="description"></div>
            </div>
        </div>


        <div class="author__products">
            <h1>Курсы автора</h1>

            <div class="author__items">
                <div class="author__item" v-for="item in products" :key="item.id">
                    <img :src="item.add_image[0].image" class="productimg" />
                    <h2>{{ item.name }}</h2>
                    <p>{{ item.short_description }}</p>

                    <ul class="dot-list" v-if="item.key_features">
                        <li v-for="(feature, index) in item.key_features.split('\r\n').slice(0, 3)" :key="index">{{ feature
                        }}
                        </li>
                    </ul>

                    <div class="price">
                        <span v-if="item.discount > 0">
                            {{ item.price.toLocaleString() + ' ₸' }}
                            <img src="@/assets/img/disc.svg" alt="" loading="lazy">
                        </span>
                        <h3 v-if="item.discount > 0">{{ (Math.floor(item.price - ((item.price * item.discount) /
                            100))).toLocaleString() + ' ₸' }}</h3>
                        <h3 v-else>{{ item.price == 0 ? 'Бесплатно' : item.price.toLocaleString() + ' ₸' }}</h3>
                    </div>

                    <div class="buttons">
                        <NuxtLink :to="'/product/' + item.id">
                            Подробнее
                        </NuxtLink>
                        <NuxtLink @click="addToCart(item.id)" style="cursor: pointer;">
                            {{ item.addToCartStatus || 'Купить' }}
                        </NuxtLink>
                    </div>
                </div>

            </div>
        </div>
    </div>
</template>
<script>
import global from '~/mixins/global';
import axios from 'axios';
export default {
    mixins: [global],
    data() {
        return {
            productId: this.$route.params.id,
            author: [],
            pathUrl: 'https://studynow.kz',
            products: [],
            addToCartStatus: '',
        }
    },
    methods: {
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
                    const index = this.products.findIndex(item => item.id === id);
                    if (response.status == 201) {
                        // Присвоение значения напрямую
                        this.products[index].addToCartStatus = 'Добавлен';
                    } else {
                        this.products[index].addToCartStatus = 'Ошибка';
                    }
                    console.log(response)
                })
                .catch(error => {
                    console.error(error)
                })
        },

        getAuthor() {
            const path = `${this.pathUrl}/api/seller/seller-this/${this.productId}`
            axios
                .get(path)
                .then(response => {
                    this.author = response.data
                    this.products = response.data.products

                })
                .catch(error => {
                    console.error(error)
                })
        }

    },
    mounted() {
        this.getAuthor()
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
.productimg {
    height: 174px;
    width: 100%;
    object-fit: cover;
    border-radius: 10px;

    @media (max-width: 1024px) {
        height: 230px;
    }
}

.author {
    padding: 120px 110px 110px;

    @media (max-width: 1600px) {
        padding: 120px 50px 110px;
    }

    @media (max-width: 1024px) {
        padding: 120px 20px 50px;
    }

    .description {
        font-size: 20px;
        font-style: normal;
        font-weight: 600;
        line-height: 130%;
        font-family: var(--int);
        color: #000;
        white-space: break-spaces;

        @media (max-width: 1024px) {
            font-size: 16px;
        }
    }


    .author__products {
        margin-top: 50px;

        @media (max-width: 1024px) {
            margin-top: 20px;
        }

        h1 {
            font-size: 40px;
            font-style: normal;
            font-weight: 500;
            line-height: 130%;
            font-family: var(--int);
            color: #000;
            margin-top: 10px;
            margin-bottom: 30px;

            @media (max-width: 1024px) {
                font-size: 24px;
            }
        }

        .author__items {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 50px;
            grid-auto-flow: dense;

            @media (max-width: 1600px) {
                gap: 35px;
                justify-content: center;
            }

            @media (max-width: 1024px) {
                gap: 20px;
            }

            .author__item {
                padding: 20px;
                border-radius: 10px;
                background: #fff;
                box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
                max-width: 300px;
                display: flex;
                flex-direction: column;

                @media (max-width: 1200px) {
                    max-width: 100%;
                    width: 100%;
                    padding: 10px;
                }

                img {
                    max-width: 100%;
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

    .author__desc {
        margin-top: 30px;
        display: flex;
        gap: 30px;

        @media (max-width: 1024px) {
            gap: 20px;
            flex-direction: column;
        }

        .avatar {
            //   border-radius: 50%;

            img {
                width: 16.563vw;
                height: 16.563vw;
                object-fit: cover;
                border-radius: 50%;

                @media (max-width: 1024px) {
                    text-align: center;
                    width: 150px;
                    height: 150px;
                }
            }
        }
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

        @media (max-width: 1024px) {
            font-size: 24px;
        }
    }


}
</style>