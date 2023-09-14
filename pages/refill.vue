<template>
    <div class="refill">
        <prevPage />

        <div class="refill__block">
            <div class="refill__body">

                <div class="text-center">
                    <h1>Пополнение баланса</h1>

                    <div class="change" v-if="accountType == 'buyer'">
                        <NuxtLink to="/refill">Пополнение</NuxtLink>
                        <NuxtLink to="/withdrawal">Вывод</NuxtLink>
                    </div>
                </div>

                <p>Порядок действий для пополнения баланса</p>

                <p>1. Подтвердите Ваше согласие с правилами нашей системы</p>

                <label class="custom-checkbox">
                    <input type="checkbox">
                    <p class="checkbox-text m-0">Я согласен с <NuxtLink to="/terms">пользовательским соглашением
                        </NuxtLink>
                        и <NuxtLink to="/polytics">политикой конфиденциальности</NuxtLink>
                    </p>
                </label>

                <p>2. Введите сумму, на которую Вы хотите пополнить личный счет, и нажмите на кнопку “Пополнить”. Вы
                    будете
                    переадресованы на сайт платежной системы, где сможете завершить платеж.</p>



                <div class="send">
                    <input type="number" v-model="count" placeholder="Введите сумму">
                    <button ref="inBtn" @click="inMoney">Пополнить</button>
                </div>

                <div class="summ">
                    <button @click="count = 100" :class="{ active: count == 100 }">100 ₸</button>
                    <button @click="count = 1000" :class="{ active: count == 1000 }">1000 ₸</button>
                    <button @click="count = 2000" :class="{ active: count == 2000 }">2000 ₸</button>
                    <button @click="count = 5000" :class="{ active: count == 5000 }">5000 ₸</button>
                    <button @click="count = 10000" :class="{ active: count == 10000 }">10000 ₸</button>
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
            count: null,
            accountType: '',
            pathUrl: 'https://studynow.kz',
            checked: false,
        }
    },
    methods: {
        inMoney() {
            const token = this.getAuthorizationCookie()
            const csrf = this.getCSRFToken()
            const path = `${this.pathUrl}/api/money/new-pay`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            this.$refs.inBtn.innerHTML = 'ОЖИДАЙТЕ'

            axios
                .post(path, {
                    amount: this.count
                })
                .then(response => {
                    console.log(response)
                    window.location.href = response.data.url
                    if (response.status = 201) {
                        this.$refs.inBtn.innerHTML = 'ПОПОЛНИТЬ'
                    }
                    if (response.status == 228) {
                        this.$refs.outBtn.innerHTML = response.data.error_msg
                    }
                })
                .catch(error => {
                    console.error(error)
                    this.$refs.inBtn.innerHTML = 'ПОПОЛНИТЬ'
                })
        },
    },
    mounted() {
        const accType = localStorage.getItem('accountType')
        if (accType !== 'buyer-account' && accType !== 'seller-account') {
            window.location.href = '/login'
        }
        if (accType == 'buyer-account') {
            this.accountType = 'buyer'

        }
        else if (accType == 'seller-account') {
            this.accountType = 'seller'
        }
        else {
            return
        }

    }

}
</script>
<script setup>
useSeoMeta({
    title: 'Вывод | Studynow',
    ogTitle: 'Вывод | Studynow',
    description: 'Вывод | Studynow',
    ogDescription: 'Вывод | Studynow',
})
</script>
<style lang="scss" scoped>
.refill {
    padding: 120px 110px 170px;


    @media (max-width: 1600px) {
        padding: 125px 50px 110px;
    }

    @media (max-width: 1024px) {
        padding: 125px 20px 50px;
    }

    .refill__block {
        display: flex;
        align-items: center;
        justify-content: center;

        .refill__body {
            margin-top: 40px;
            border-radius: 10px;
            background: #FFF;
            box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
            padding: 40px;

            @media (max-width: 1024px) {
                padding: 20px;
            }

            .change {
                display: flex;

                a {
                    flex: 1;
                    padding: 12px 0;
                    background: transparent;
                    border-radius: 10px;
                    border: 2px solid #000;
                    text-decoration: none;

                    font-size: 24px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 110%;
                    font-family: var(--int);

                    @media (max-width: 1024px) {
                        font-size: 18px;
                    }
                }

                a:first-child {
                    border-top-right-radius: 0;
                    border-bottom-right-radius: 0;
                    border-right: 0;

                    color: #fff;
                    background: #000;
                }

                a:last-child {
                    border-top-left-radius: 0;
                    border-bottom-left-radius: 0;
                    border-left: 0;


                }
            }

            .summ {
                margin-top: 20px;
                display: flex;
                flex-wrap: wrap;
                gap: 10px;

                @media (max-width: 1024px) {
                    justify-content: center;
                }

                .active {
                    color: #fff;
                    background: #000;
                }

                button {
                    padding: 13px;
                    background: transparent;
                    border-radius: 10px;
                    border: 2px solid #000;

                    font-size: 20px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: normal;
                    color: #000;
                    font-family: var(--int);
                    transition: all .3s ease;

                    @media (max-width: 1024px) {
                        font-size: 16px;
                    }
                }
            }

            .send {
                display: flex;
                gap: 20px;

                input {
                    width: 100%;
                    max-width: 227px;
                    border-radius: 10px;
                    border: 2px solid #000;
                    padding: 12px;
                    text-align: right;

                    font-size: 20px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #000;

                    @media (max-width: 1024px) {
                        font-size: 16px;
                        max-width: 150px;
                    }

                    @media (max-width: 360px) {
                        max-width: 100px;
                    }
                }

                button {
                    padding: 12px 0;
                    flex: 1;
                    background: #000;
                    border: 0;
                    border-radius: 10px;

                    font-size: 20px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #fff;

                    @media (max-width: 1024px) {
                        font-size: 16px;
                    }

                    &:hover {
                        background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
                    }
                }
            }

            h1 {
                font-size: 32px;
                font-style: normal;
                font-weight: 500;
                line-height: normal;
                font-family: var(--int);
                color: #000;
                margin-bottom: 25px;

                @media (max-width: 1024px) {
                    font-size: 25px;
                }
            }

            p,
            a {
                margin-bottom: 25px;
                font-size: 20px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
                max-width: 489px;

                @media (max-width: 1024px) {
                    font-size: 16px;
                }
            }

            a {
                text-decoration: underline;
            }
        }
    }

}

.custom-checkbox p {
    font-family: var(--int);
    font-size: 20px;
    font-style: normal;
    font-weight: 500;
    line-height: 130%;
    color: #000;
    max-width: 489px;

    @media (max-width: 1024px) {
        font-size: 16px;
    }
}

.custom-checkbox input[type="checkbox"] {
    opacity: 0;
    position: absolute;
    border-radius: 3px;
}

.custom-checkbox .checkbox-text:before {
    content: '';
    display: inline-block;
    vertical-align: middle;
    width: 20px;
    height: 20px;
    margin-right: 10px;
    border: 2px solid #3C3C3C;
    border-radius: 4px;
    margin-bottom: 4px;
}

.custom-checkbox input[type="checkbox"]:checked+.checkbox-text:before {
    content: url('@/assets/img/check.svg');
    font-size: 16px;
    color: black;
    text-align: center;
    line-height: 20px;
    background: transparent;
}

.custom-checkbox {
    margin-bottom: 22px;
}

.custom-checkbox:last-child {
    margin-bottom: 0 !important;
}
</style>