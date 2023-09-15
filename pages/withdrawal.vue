<template>
    <div class="withdrawal">
        <prevPage />

        <div class="withdrawal__block">
            <div class="withdrawal__body">

                <div class="text-center">
                    <h1>Вывод средств</h1>

                    <div class="change" v-if="accountType == 'buyer'">
                        <NuxtLink to="/refill">Пополнение</NuxtLink>
                        <NuxtLink to="/withdrawal">Вывод</NuxtLink>
                    </div>
                </div>

                <p>Порядок действий для вывода средств</p>

                <p>1. Подтвердите Ваше согласие с правилами нашей системы</p>

                <label class="custom-checkbox">
                    <input type="checkbox">
                    <p class="checkbox-text m-0">Я согласен с <NuxtLink to="/terms">пользовательским соглашением</NuxtLink>
                        и <NuxtLink to="/polytics">политикой конфиденциальности</NuxtLink>
                    </p>
                </label>

                <p>2. Введите сумму, которую Вы хотите вывести с личного счета, и нажмите на кнопку “Вывести”. Вы будете
                    переадресованы на сайт платежной системы, где сможете завершить операцию.</p>
                <div class="card">
                    <input type="text" class="mb-3 w-100" name="card" id="card" v-model="cardNumber"
                        :maxlength="cardNumberMaxLength" placeholder="Введите номер карты" @input="formatCardNumber"
                        autocomplete="cc-number">
                    <input type="text" class="mb-3 w-100" name="cardHolder" id="card" v-model="cardHolder"
                        placeholder="Введите владельца карты" autocomplete="cc-name">
                </div>
                <div class="send">
                    <input type="number" v-model="count" placeholder="Введите сумму">
                    <button ref="outBtn" @click="outMoney">Вывести</button>
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
import axios from 'axios';
export default {
    mixins: [global],
    data() {
        return {
            count: null,
            pathUrl: 'https://studynow.kz',
            cardNumber: '',
            cardHolder: '',
            cardNumberMaxLength: 19,
            accountType: '',
            checked: false,
        }
    },
    methods: {
        outMoney() {
            const token = this.getAuthorizationCookie()
            const csrf = this.getCSRFToken()
            const path = `${this.pathUrl}/api/money/pay-return`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            this.$refs.outBtn.innerHTML = 'ОЖИДАЙТЕ'

            axios
                .post(path, {
                    amount: this.count,
                    card_number: this.cardNumber.replace(/\s/g, ''),
                    cardholder: this.cardHolder
                })
                .then(response => {
                    console.log(response)
                    if (response.status == 200) {
                        this.$refs.outBtn.innerHTML = 'УСПЕШНО'
                    }
                    if (response.status == 228) {
                        this.$refs.outBtn.innerHTML = response.data.error_msg
                    }

                })
                .catch(error => {
                    console.error(error)
                    this.$refs.outBtn.innerHTML = 'ВЫВЕСТИ'
                })
        },
        formatCardNumber() {
            this.cardNumber = this.cardNumber.replace(/\D/g, '');
            this.cardNumber = this.cardNumber.replace(/(.{4})/g, '$1 ');
            this.cardNumber = this.cardNumber.slice(0, this.cardNumberMaxLength);
        }
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

    },
    watch: {
        cardNumber(newCardNumber) {
            this.cardHolder = this.cardNumberToHolderMapping[newCardNumber] || "";
        }
    }

}
</script>
<script setup>
useSeoMeta({
    title: 'Пополнение | Studynow',
    ogTitle: 'Пополнение | Studynow',
    description: 'Пополнение | Studynow',
    ogDescription: 'Пополнение | Studynow',
})
</script>
<style lang="scss" scoped>
.card {
    background: 0;
    border: 0;

    input {
        background: transparent;
        border: 2px solid #000;
        padding: 10px 15px;
        border-radius: 10px;

        font-size: 18px;
        font-family: var(--int);
        color: #000;
    }
}

.withdrawal {
    padding: 120px 110px 170px;

    @media (max-width: 1600px) {
        padding: 125px 50px 110px;
    }

    @media (max-width: 1024px) {
        padding: 125px 20px 50px;
    }

    .withdrawal__block {
        display: flex;
        align-items: center;
        justify-content: center;

        .withdrawal__body {
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


                }

                a:last-child {
                    border-top-left-radius: 0;
                    border-bottom-left-radius: 0;
                    border-left: 0;
                    color: #fff;
                    background: #000;
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