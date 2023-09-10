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
            <div class="text-center">
                <button @click="activeTab = 5">
                    Добавить товар
                </button>
            </div>
            <div class="products__body">
                <div class="products__item">
                    <small>1.</small>
                    <img src="@/assets/img/myproduct.png" alt="" loading="lazy">

                    <div class="product__full">
                        <div>
                            <h1>Курс «Блюда высокой кухни со всех стран»</h1>
                            <small>11 540 ₸</small>
                        </div>


                        <div class="buttons">
                            <button @click="activeTab = 6">Изменить</button>
                            <button>Страница товара</button>
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

                        <div class="buttons">
                            <button @click="activeTab = 6">Изменить</button>
                            <button>Страница товара</button>
                        </div>
                    </div>

                </div>
            </div>
        </div>
        <div class="myproducts" v-if="activeTab == 1">

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
                            <span>Дата продажи: 01.08.23</span>
                        </div>

                        <div class="buttons">
                            <button>Чат с покупателем</button>
                            <button>Страница товара</button>
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
                            <span>Дата продажи: 01.08.23</span>
                        </div>

                        <div class="buttons">
                            <button>Чат с покупателем</button>
                            <button>Страница товара</button>
                        </div>
                    </div>

                </div>
            </div>
        </div>

        <div class="chats" v-if="activeTab == 3">

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

        <div class="accs" v-if="activeTab == 4">
            <div class="account__profile">
                <div class="profile__left">
                    <div class="avatar w-100">
                        <div>
                            <img src="@/assets/img/avatarlc.png" alt="" loading="lazy">

                            <div class="editava">
                                <span>Изменить фото</span>
                            </div>
                        </div>
                        <div class="">
                            <label for="name">Отображаемое Имя</label>
                            <input type="text" placeholder="Ваше имя">
                        </div>
                    </div>

                    <div class="data">
                        <label for="name">E-mail</label>
                        <input class="w-100" type="email" placeholder="E-mail">
                    </div>

                    <div class="data">
                        <label for="name">Пароль</label>
                        <input class="w-100" type="password" placeholder="Пароль">
                    </div>

                </div>
                <div class="profile__right w-100">
                    <label for="desc">Описание профиля</label>
                    <textarea name="desc" id="desc" cols="30" rows="17"></textarea>
                </div>
            </div>

            <div class="buttons">
                <button>Сохранить изменения</button>
                <button>Выйти из аккаунта</button>
            </div>
        </div>

        <TheTrans v-if="activeTab == 2"></TheTrans>
        <CreateProduct v-if="activeTab == 5"></CreateProduct>
        <EditProduct v-if="activeTab == 6"></EditProduct>
        <TheMessanger v-if="activeTab == 7"></TheMessanger>
    </div>
</template>
<script>
export default {
    data() {
        return {
            tabs: ['Мои товары', 'Мои продажи', 'Транзакции', 'Обратная связь', 'Аккаунт'],
            activeTab: 0,
            tabWidth: 0,
            tabOffset: 0,
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

    }
    ,
    mounted() {
        this.updateHighlightPosition(this.activeTab);
    },
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

    .accs {
        .buttons {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 20px;
            margin-top: 30px;

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

    .account__profile {
        margin-top: 38px;
        display: flex;
        gap: 20px;

        label,
        input {
            display: block;
        }

        label {
            font-size: 16px;
            font-style: normal;
            font-weight: 500;
            line-height: 110%;
            font-family: var(--int);
            color: #000;
            margin-left: 10px;
        }

        input {
            border: 2px solid #000;
            border-radius: 10px;
            padding: 10px;
            width: 336px;
            max-width: 527px;

            font-size: 16px;
            font-style: normal;
            font-weight: 400;
            line-height: 130%;
            font-family: var(--int);
            color: #000;
            background: transparent;
        }


        .profile__left {
            // width: 100%;

            .data {
                margin-top: 20px;
            }

            .avatar {
                display: flex;
                gap: 20px;
                align-items: start;

                img {
                    max-width: 171px;
                    max-height: 171px;
                }

                div {
                    position: relative;
                    overflow: hidden;


                    .editava {
                        position: absolute;
                        display: flex;
                        justify-content: center;
                        transition: all .3s ease;
                        transform: scaleY(0);
                        width: 100%;
                        height: 100%;
                        border-radius: 50%;
                        background: rgba(255, 255, 255, 0.50);
                        cursor: pointer;

                        top: 0;

                        span {
                            display: flex;
                            align-items: center;

                            font-size: 10.755px;
                            font-style: normal;
                            font-weight: 500;
                            line-height: 130%;
                            text-decoration-line: underline;
                            font-family: var(--int);
                            color: #000;
                            cursor: pointer;
                        }

                    }

                    &:hover .editava {
                        transform: scaleY(1)
                    }
                }
            }
        }

        .profile__right {
            textarea {
                width: 100%;
                display: block;
                background: transparent;
                border-radius: 10px;
                border: 2px solid #000;
                padding: 20px;

                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
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