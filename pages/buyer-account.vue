<template>
    <div class="account">
        <h1>Личный кабинет</h1>

        <div class="account__nav">
            <span v-for="(tab, index) in tabs" :key="index" :class="{ 'nav-item': true, active: activeTab === index }"
                @click="changeTab(index)">
                {{ tab }}
            </span>
            <div class="highlight" :style="{ width: tabWidth + 'px', transform: 'translateX(' + tabOffset + 'px)' }"></div>
        </div>

        <div class="myproducts" v-if="activeTab == 0">

            <div class="products__body">
                <div class="products__item">
                    <small>1.</small>
                    <img src="@/assets/img/myproduct.png" alt="" loading="lazy">

                    <div class="product__full">
                        <div>
                            <h1>Курс «Блюда высокой кухни со всех стран»</h1>
                            <small>11 540 ₸</small>
                        </div>

                        <div>
                            <span>Дата покупки: 01.08.23</span>
                        </div>

                        <div class="buttons">
                            <button>Чат с продавцом</button>
                            <button>Скачать файл</button>
                        </div>
                    </div>

                </div>
                <div class="products__item">
                    <small>2.</small>
                    <img src="@/assets/img/myproduct.png" alt="" loading="lazy">

                    <div class="product__full">
                        <div>
                            <h1>Курс «Блюда высокой кухни со всех стран»</h1>
                            <small>11 540 ₸</small>
                        </div>

                        <div>
                            <span>Дата покупки: 01.08.23</span>
                        </div>

                        <div><span>АВТОР: <span class="mb-0" style="text-decoration: underline; text-transform: none;">Анна
                                    Скобина</span></span></div>

                        <div class="buttons">
                            <button>Чат с продавцом</button>
                            <button>Скачать файл</button>
                        </div>
                    </div>

                </div>
            </div>
        </div>

        <div class="chats" v-if="activeTab == 2">

            <div class="chat__item">
                <div>
                    <h2>alex.ivanov@gmail.com</h2>
                    <small>23.07.2023 14:47</small>
                </div>

                <div class="justify-content-end">
                    <button @click="activeTab = 7">Открыть чат</button>
                </div>
            </div>

            <div class="chat__item">
                <div>
                    <h2>alex.ivanov@gmail.com</h2>
                    <small>23.07.2023 14:47</small>
                </div>

                <div class="justify-content-end">
                    <button @click="activeTab = 7">Открыть чат</button>
                </div>
            </div>

            <div class="chat__item">
                <div>
                    <h2>alex.ivanov@gmail.com</h2>
                    <small>23.07.2023 14:47</small>
                </div>

                <div class="justify-content-end">
                    <button @click="activeTab = 7">Открыть чат</button>
                </div>
            </div>

        </div>

        <div class="profile" v-if="activeTab == 3">
            <div>
                <div class="inputs">
                    <div>
                        <label for="email">E-mail</label>
                        <input type="email" id="email" v-model="email">
                    </div>
                    <div>
                        <label for="password">Пароль</label>
                        <input type="password" id="password" v-model="password">
                    </div>
                </div>
                <div class="text-center">
                    <button>Выйти из аккаунта</button>
                </div>
            </div>
        </div>
        <TheMessanger v-if="activeTab == 7"></TheMessanger>
        <TheTrans v-if="activeTab == 1"></TheTrans>
    </div>
</template>
<script>
export default {
    data() {
        return {
            tabs: ['Мои покупки', 'Транзакции', 'Обратная связь', 'Аккаунт'],
            activeTab: 0,
            tabWidth: 0,
            tabOffset: 0,
            email: '',
            password: '',
        }
    },
    methods: {
        changeTab(index) {
            this.activeTab = index;
            this.updateHighlightPosition(index);
        },
        updateHighlightPosition(index) {
            const tabs = this.$el.querySelectorAll('.nav-item');
            this.tabWidth = tabs[index].offsetWidth;
            this.tabOffset = tabs[index].offsetLeft;
        },
    },
    mounted() {
        this.updateHighlightPosition(this.activeTab);
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Личный кабинет | Studynow',
    ogTitle: 'Личный кабинет | Studynow',
    description: 'Личный кабинет | Studynow',
    ogDescription: 'Личный кабинет | Studynow',
})
</script>
<style lang="scss" scoped>
.account {
    padding: 125px 110px 72px;

    .profile {
        display: flex;
        align-items: center;
        justify-content: center;
        margin: 150px 0;

        .inputs {
            display: flex;
            gap: 20px;

            input,
            label {
                display: block;
            }

            label {
                margin-left: 10px;
                font-size: 20px;
                font-style: normal;
                font-weight: 400;
                line-height: 110%;
                font-family: var(--int);
                color: #000;
            }

            input {
                background: transparent;
                border: 2px solid #000;
                border-radius: 10px;
                padding: 10px 15px;

                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
                width: 23.438vw;
            }
        }

        button {
            margin-top: 30px;
            border-radius: 10px;
            background: #000;
            border: 0;
            padding: 10px 30px;

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


    .chats {
        margin-top: 38px;
        display: flex;
        flex-wrap: wrap;
        gap: 30px;

        .chat__item {
            border-radius: 10px;
            background: #FFF;
            box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
            padding: 30px 20px;
            width: 546px;

            div {
                display: flex;
                justify-content: space-between;
                align-items: center;
                width: 100%;

                h2 {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: normal;
                    font-family: var(--int);
                    color: #000;
                    margin: 0;
                }

                small {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #000;
                }
            }

            button {
                padding: 10px 30px;
                border: 0;
                border-radius: 10px;
                background: #000;
                margin-top: 30px;

                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                color: #fff;

                &:hover {
                    background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
                }
            }
        }
    }

    .myproducts {
        margin-top: 38px;

        transition: all .3s ease;

        .products__body {
            .products__item {
                display: flex;
                margin-bottom: 30px;

                &:last-child {
                    margin-bottom: 0;
                }

                img {
                    max-width: 470px;
                    max-height: 308px;
                }

                .product__full {
                    margin-left: 60px;
                    width: 100%;

                    .buttons {
                        display: flex;
                        justify-content: flex-end;
                        align-items: center;
                        gap: 20px;

                        margin-top: 100px;


                    }

                    span {
                        font-size: 24px;
                        font-style: normal;
                        font-weight: 400;
                        line-height: 110%;
                        text-transform: uppercase;
                        font-family: var(--int);
                        color: #000;
                        margin-top: 30px;
                    }

                    div {
                        display: flex;
                        justify-content: space-between;
                        align-items: center;
                        width: 100%;

                        h1 {
                            font-size: 24px;
                            font-style: normal;
                            font-weight: 500;
                            line-height: normal;
                            text-transform: uppercase;
                            font-family: var(--int);
                            color: #000;
                            margin: 0;

                        }

                        small {
                            font-size: 40px;
                            font-style: normal;
                            font-weight: 400;
                            line-height: normal;
                            text-transform: uppercase;
                            font-family: var(--int);
                            color: #000;
                            margin: 0;
                        }
                    }
                }

                small {
                    margin-right: 27px;
                    margin-top: 15px;
                    font-size: 24px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: normal;
                    text-transform: uppercase;
                    font-family: var(--int);
                    color: #000;
                }
            }
        }

        button {
            padding: 10px 30px;
            border-radius: 10px;
            background: #000;
            border: 0;
            margin-bottom: 34px;

            font-size: 16px;
            font-style: normal;
            font-weight: 400;
            line-height: 130%;
            color: #fff;

            &:hover {
                background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
            }
        }
    }

    .account__nav {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 66px;
        margin-top: 20px;
        position: relative;

        .nav-item {
            cursor: pointer;
            padding: 10px;
            text-align: center;
            // flex: 1;
        }

        span {
            cursor: pointer;
            font-size: 20px;
            font-style: normal;
            font-weight: 400;
            line-height: 110%;
            font-family: var(--int);
            color: #000;
        }

        .highlight {
            position: absolute;
            bottom: 0;
            left: 0;
            height: 3px;
            background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
            transition: 0.3s ease;
        }

        .active {}
    }

    h1 {
        font-size: 40px;
        font-style: normal;
        font-weight: 500;
        line-height: normal;
        font-family: var(--int);
        color: #000;
    }
}
</style>