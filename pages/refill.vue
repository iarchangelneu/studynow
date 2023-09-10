<template>
    <div class="refill">
        <prevPage />

        <div class="refill__block">
            <div class="refill__body">

                <div class="text-center">
                    <h1>Пополнение баланса</h1>

                    <div class="change">
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
                    <button>Пополнить</button>
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
export default {
    data() {
        return {
            count: null,
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
    title: 'Вывод | Studynow',
    ogTitle: 'Вывод | Studynow',
    description: 'Вывод | Studynow',
    ogDescription: 'Вывод | Studynow',
})
</script>
<style lang="scss" scoped>
.refill {
    padding: 120px 110px 170px;

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