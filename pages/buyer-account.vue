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

        <div class="mobnav">
            <div class="row">
                <button :class="{ activebtn: activeTab == 0 || activeTab == 5 || activeTab == 6 }" @click="changeTab(0)">
                    <span :class="{ activespan: activeTab == 0 || activeTab == 5 || activeTab == 6 }">
                        Мои покупки</span>
                </button>
                <button :class="{ activebtn: activeTab == 1 }" @click="changeTab(1)">
                    <span :class="{ activespan: activeTab == 1 }">Транзакции</span>
                </button>
            </div>
            <div class="row">
                <button :class="{ activebtn: activeTab == 2 || activeTab == 7 }" @click="changeTab(2)">
                    <span :class="{ activespan: activeTab == 2 || activeTab == 7 }">Обратная связь</span>
                </button>
                <button :class="{ activebtn: activeTab == 3 }" @click="changeTab(3)">
                    <span :class="{ activespan: activeTab == 3 }">Аккаунт</span>
                </button>
            </div>

        </div>

        <div class="myproducts" v-if="activeTab == 0">

            <div class="products__body">
                <div class="products__item" v-for="(item, i) in buys" :key="item.id">
                    <small>{{ i + 1 }}.</small>
                    <img :src="item.products.add_image[0].image" class="bigimg" alt="" loading="lazy">

                    <div class="product__full">
                        <div>
                            <h1>{{ item.products.name }}</h1>
                            <small>{{ item.products.price == 0 ? 'Бесплатно' : (Math.floor(item.products.price -
                                ((item.products.price * item.products.discount) /
                                    100))).toLocaleString() + ' ₸'
                            }}</small>
                        </div>

                        <div>
                            <span>Дата покупки: {{ formatDate(item.date) }}</span>
                        </div>

                        <div class="buttons">
                            <button @click="createChat(item.seller.id, item.seller.user.first_name)">Чат с
                                продавцом</button>

                        </div>
                    </div>

                </div>

            </div>
        </div>

        <div class="chats" v-if="activeTab == 2">
            <div class="chat__item" v-for="chat in chats" :key="chat.id">
                <div>
                    <h2>{{ chat.seller.user.first_name }}</h2>
                    <!-- <small>23.07.2023 14:47</small> -->
                </div>

                <div class="justify-content-end">
                    <button @click="openChat(chat.id, chat.seller.user.first_name)">Открыть чат</button>
                </div>
            </div>



        </div>

        <div class="profile" v-if="activeTab == 3">
            <div class="ttrds">
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
                    <button @click="logOut()">Выйти из аккаунта</button>
                </div>
            </div>
        </div>
        <TheMessanger v-if="activeTab == 7" :chatId="chatId" :name="chatName"></TheMessanger>
        <TheTrans v-if="activeTab == 1" :transactions="transactions"></TheTrans>
    </div>
</template>
<script>
import global from '~/mixins/global';
import axios from 'axios';
export default {
    mixins: [global],
    data() {
        return {
            tabs: ['Мои покупки', 'Транзакции', 'Обратная связь', 'Аккаунт'],
            activeTab: 0,
            tabWidth: 0,
            tabOffset: 0,
            email: '',
            password: '',
            chats: [],
            seller: [],
            pathUrl: 'https://studynow.kz',
            buys: [],
            sendId: null,
            chatId: null,
            myId: null,
            transactions: []
        }
    },
    methods: {
        formatDate(dateString) {
            const date = new Date(dateString);
            const formattedDate = `${date.getDate().toString().padStart(2, '0')}.${(date.getMonth() + 1).toString().padStart(2, '0')}.${date.getFullYear()}`;
            return formattedDate;
        },
        getAccount() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/buyer/buyer-lk`;
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios
                .get(path)
                .then(response => {
                    this.account = response.data
                    this.myId = response.data.id
                    this.transactions = response.data.transactions
                    this.email = response.data.user.email

                })
                .catch(error => console.log(error));
        },
        openChat(chatId, chatName) {
            this.activeTab = 7;
            this.chatId = chatId;
            this.chatName = chatName
        },
        getBuys() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/buyer/buyer-lk/my-purchases`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios
                .get(path)
                .then(response => {
                    this.buys = response.data
                })
                .catch(error => {
                    console.error(error)
                })
        },
        createChat(id, name) {
            const token = this.getAuthorizationCookie()
            const csrf = this.getCSRFToken()
            const path = `${this.pathUrl}/api/messanger/new-chat`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            axios
                .post(path, {
                    buyer: this.myId,
                    seller: id,
                })
                .then(response => {
                    const chatId = response.data.chat_id
                    this.openChat(chatId, name)
                })
                .catch(error => console.log(error))
        },
        getChats() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/messanger/all-chats`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios
                .get(path)
                .then(res => {
                    this.chats = res.data
                })
                .catch(error => console.log(error))
        },
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

        const accType = localStorage.getItem('accountType')
        console.log(accType)
        if (accType == 'buyer-account') {
            this.getAccount()
            this.getChats()
            this.getBuys()
        }
        else {
            window.location.href = '/login'
        }
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
.bigimg {

    min-width: 470px;
    height: 308px;
    border-radius: 10px;
    object-fit: cover;

    @media (max-width: 1024px) {
        min-width: 100%;
        height: 230px;
    }

}

.account {
    padding: 125px 110px 72px;

    @media (max-width: 1600px) {
        padding: 125px 50px 72px;
    }

    @media (max-width: 1024px) {
        padding: 125px 20px 50px;
    }

    .profile {
        display: flex;
        align-items: center;
        justify-content: center;
        margin: 150px 0;

        @media (max-width: 1024px) {
            margin: 30px 0;
        }

        .ttrds {
            @media (max-width: 1024px) {
                width: 100%;
            }
        }

        .inputs {
            display: flex;
            gap: 20px;

            @media (max-width: 1024px) {
                flex-direction: column;
                width: 100%;
            }

            input,
            label {
                display: block;
            }

            div {
                width: 100%;
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

                @media (max-width: 1024px) {
                    width: 100%;
                }
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

                @media (max-width: 1024px) {
                    flex-direction: column;
                    width: 100%;
                    margin-bottom: 20px;
                }

                small {
                    @media (max-width: 1024px) {
                        &:first-child {
                            display: none;
                        }

                    }
                }

                &:last-child {
                    margin-bottom: 0;
                }



                .product__full {
                    margin-left: 60px;
                    width: 100%;

                    @media (max-width: 1024px) {
                        margin: 0;
                    }

                    .buttons {
                        display: flex;
                        justify-content: flex-end;
                        align-items: center;
                        gap: 20px;

                        margin-top: 100px;

                        @media (max-width: 1024px) {
                            margin-top: 10px;
                        }


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

                        @media (max-width: 1024px) {
                            margin-top: 10px;
                            font-size: 16px;
                        }
                    }

                    div {
                        display: flex;
                        justify-content: space-between;
                        align-items: center;
                        width: 100%;

                        @media (max-width: 1024px) {
                            &:first-child {
                                flex-direction: column;
                                align-items: flex-start;
                                margin-top: 10px;
                                gap: 10px;
                            }

                        }

                        h1 {
                            font-size: 24px;
                            font-style: normal;
                            font-weight: 500;
                            line-height: normal;
                            text-transform: uppercase;
                            font-family: var(--int);
                            color: #000;
                            margin: 0;

                            @media (max-width: 1600px) {
                                text-transform: none;
                                font-size: 18px;
                            }

                            @media (max-width: 1024px) {
                                font-size: 16px;
                                text-transform: none;
                            }

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

                            @media (max-width: 1600px) {
                                text-transform: none;
                                font-size: 30px;
                            }

                            @media (max-width: 1024px) {
                                font-size: 24px;
                            }
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

    .mobnav {
        display: none;

        @media (max-width: 1024px) {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            flex-direction: column;
            padding: 0 15px;

            .row {
                display: flex;
                gap: 10px;
            }

            .activebtn {
                background: #FCF0FF !important;
                box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10) !important;
            }

            .activespan {
                background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
                background-clip: text;
                -webkit-background-clip: text;
                -webkit-text-fill-color: transparent;

            }

            button {
                flex: 1;
                border: 0;
                border-radius: 10px;
                background: #fff;
                box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
                padding: 15px 0;

                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
                height: 50px;
                transition: all .3s ease;

                span {
                    transition: all .3s ease;
                }

                // &:last-child {
                //     width: 100%;
                // }
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

        @media (max-width: 1024px) {
            display: none;
        }

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

        @media (max-width: 1024px) {
            font-size: 24px;
        }
    }
}
</style>