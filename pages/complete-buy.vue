<template>
    <div class="complete">
        <prevPage />

        <h1>Корзина</h1>

        <div class="complete__body">
            <div class="cart">
                <div class="cart__item" v-for="item in cart" :key="item.id">
                    <img :src="pathUrl + '/api' + item.products.add_image[0].image" class="cartimg" alt="" loading="lazy">

                    <div>
                        <h2>{{ item.products.name }}</h2>
                        <div class="price">
                            <h3 v-if="item.products.discount > 0">
                                {{ item.products.price.toLocaleString() + ' ₸' }}
                                <img src="@/assets/img/disc.svg" alt="">
                            </h3>
                            <h2 v-if="item.products.discount > 0">
                                {{ (Math.floor(item.products.price - ((item.products.price * item.products.discount) /
                                    100))).toLocaleString() + ' ₸'
                                }}</h2>
                            <h2 v-else>{{ item.products.price == 0 ? 'Бесплатно' : item.products.price.toLocaleString() +
                                '₸' }}</h2>
                        </div>
                        <div class="text-right">
                            <img src="@/assets/img/trashbig.svg" @click="deleteFromCart(item.id)" alt=""
                                style="cursor: pointer;">
                        </div>
                    </div>
                </div>
            </div>

            <div class="complete__block">
                <h1>Подтверждение покупки</h1>

                <h2>Количество курсов: {{ cart.length }}</h2>
                <h2>Итоговая сумма: {{ formatPrice(calculateTotal()) }} ₸ </h2>

                <p>Сумма будет списана с вашего счета. Товары отобразятся во вкладке «Мои покупки» в Вашем Личном кабинете.
                </p>

                <div class="text-center">
                    <button ref="buyBtn" @click="buyProduct()">Подтвердить покупку</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import global from '~/mixins/global';
import axios from 'axios'
export default {
    mixins: [global],
    data() {
        return {
            cart: [],
        }
    },
    methods: {
        buyProduct() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/buyer/placed-basket`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            this.$refs.buyBtn.innerHTML = 'Оформляем'
            axios
                .get(path)
                .then(response => {
                    console.log(response)
                    this.getCart()
                    if (response.status == 204) {
                        this.$refs.buyBtn.innerHTML = 'Недостаточно средств'
                    }
                    if (response.status == 201) {
                        // this.getBuyer()
                        this.$refs.buyBtn.innerHTML = 'Оплата прошла успешно'

                        setTimeout(() => {
                            window.location.href = '/catalog'
                        }, 3);
                    }
                })
                .catch(error => {
                    console.error(error)
                })

        },
        calculateTotal() {
            let total = 0;

            this.cart.forEach(item => {
                const { price, discount } = item.products;
                const discountedPrice = price * (1 - discount / 100); // Преобразуем скидку в коэффициент
                total += discountedPrice * item.amount;
            });

            return total;
        },
        formatPrice(price) {
            return price.toLocaleString('ru-RU');
        },
        deleteFromCart(id) {
            const token = this.getAuthorizationCookie()
            const csrf = this.getCSRFToken()
            const path = `${this.pathUrl}/api/buyer/delete-product-basket/${id}`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            axios
                .put(path)
                .then(response => {
                    console.log(response)
                    this.getCart()
                })
                .catch(error => {
                    console.error(error)
                })
        },
        getCart() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/buyer/all-product-basket`;
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;

            axios
                .get(path)
                .then(response => {
                    this.cart = response.data
                })
                .catch(error => {
                    console.error(error)
                })
        },
    },
    mounted() {
        this.getCart()
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Подтверждение покупки | Studynow',
    ogTitle: 'Подтверждение покупки | Studynow',
    description: 'Подтверждение покупки | Studynow',
    ogDescription: 'Подтверждение покупки | Studynow',
})
</script>
<style lang="scss" scoped>
.cartimg {
    min-width: 220px;
    height: 144px;
    object-fit: cover;
    border-radius: 10px;

    @media (max-width: 1024px) {
        width: 100%;
        height: 230px;
    }
}

.complete {
    padding: 120px 110px 150px;


    @media (max-width: 1600px) {
        padding: 125px 50px 110px;
    }

    @media (max-width: 1024px) {
        padding: 125px 20px 50px;
    }


    .complete__body {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;

        @media (max-width: 1400px) {
            flex-direction: column;
            justify-content: center;
            align-items: center;
            gap: 50px;
            width: 100%;
        }

        .complete__block {
            border-radius: 10px;
            background: var(--White, #FFF);
            box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
            padding: 20px 40px 34px;

            @media (max-width: 1024px) {
                padding: 15px;
            }

            h1 {
                text-align: center;
                font-size: 32px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                margin-bottom: 40px;

                @media (max-width: 1024px) {
                    font-size: 20px;
                }
            }

            h2 {
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
                margin-bottom: 20px;

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
                margin-bottom: 40px;
                max-width: 520px;

                @media (max-width: 1024px) {
                    font-size: 14px;
                }
            }

            button {
                padding: 12px 66px;
                background: #000;
                border-radius: 10px;
                border: 0;

                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #fff;

                @media (max-width: 1024px) {
                    font-size: 16px;
                    padding: 10px 30px;
                }

                &:hover {
                    background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
                }
            }
        }

        .cart {
            display: flex;
            flex-direction: column;
            gap: 50px;
            width: 80%;

            @media (max-width: 1400px) {
                width: 100%;
                justify-content: center;
            }

            @media (max-width: 1024px) {
                gap: 20px;
            }
        }

        .cart__item {
            display: flex;
            gap: 30px;

            width: 500px;

            @media (max-width: 1400px) {
                width: 100%;
                justify-content: space-evenly;
            }

            @media (max-width: 1024px) {
                flex-direction: column;
                gap: 20px;
            }



            .price {
                @media (max-width: 1024px) {
                    display: flex;
                    gap: 10px;
                    align-items: center;
                }

            }

            div {
                width: 100%;

                h2 {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #000;
                    margin-bottom: 10px;

                    @media (max-width: 1024px) {
                        font-size: 16px;
                    }
                }

                h3 {
                    font-size: 16px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #000;
                    position: relative;
                    margin-bottom: 13px;

                    @media (max-width: 1024px) {
                        margin: 0;
                        font-size: 14px;
                    }

                    img {
                        position: absolute;
                        left: 0;
                    }
                }

                h2:nth-child(2) {
                    margin: 0;
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
        margin-bottom: 30px;
        margin-top: 10px;
    }
}
</style>