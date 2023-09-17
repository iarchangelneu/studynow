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
                        Мои товары</span>
                </button>
                <button :class="{ activebtn: activeTab == 1 }" @click="changeTab(1)">
                    <span :class="{ activespan: activeTab == 1 }">Мои продажи</span>
                </button>
            </div>
            <div class="row">
                <button :class="{ activebtn: activeTab == 2 }" @click="changeTab(2)">
                    <span :class="{ activespan: activeTab == 2 }">Транзакции</span>
                </button>
                <button :class="{ activebtn: activeTab == 3 || activeTab == 7 }" @click="changeTab(3)">
                    <span :class="{ activespan: activeTab == 3 || activeTab == 7 }">Обратная связь</span>
                </button>
            </div>
            <div class="row">
                <button :class="{ activebtn: activeTab == 4 }" @click="changeTab(4)">
                    <span :class="{ activespan: activeTab == 4 }">Аккаунт</span>
                </button>
            </div>
        </div>


        <div class="myproducts" v-if="activeTab == 0">
            <div class="text-center">
                <button @click="activeTab = 5">
                    Добавить товар
                </button>
            </div>
            <div class="products__body">
                <div class="products__item" v-for="(product, i) in products" :key="product.id">
                    <small>{{ i + 1 }}.</small>
                    <img v-if="product.add_image && product.add_image.length > 0"
                        :src="pathUrl + '/api' + product.add_image[0].image" alt="" class="bigimg" loading="lazy">
                    <div class="product__full">
                        <div>
                            <h1>{{ product.name }}</h1>
                            <small>{{ product.price == 0 ? 'Бесплатно' : (Math.floor(product.price - ((product.price *
                                product.discount) / 100))).toLocaleString() + ' ₸' }}</small>
                        </div>


                        <div class="buttons">
                            <button @click='openEditTab(product.id)'>Изменить</button>
                            <NuxtLink :to="'/product/' + product.id">Страница товара</NuxtLink>
                        </div>
                    </div>

                </div>
            </div>
        </div>
        <div class="myproducts" v-if="activeTab == 1">

            <div class="products__body">
                <div class="products__item" v-for="(item, i) in sales" :key="item.id">
                    <small>{{ i + 1 }}.</small>
                    <img v-if="item.products.add_image && item.products.add_image.length > 0"
                        :src="pathUrl + '/api' + item.products.add_image[0].image" alt="" class="bigimg" loading="lazy">

                    <div class="product__full">
                        <div>
                            <h1>{{ item.products.name }}</h1>
                            <small>{{ item.products.price == 0 ? 'Бесплатно' : (Math.floor(item.products.price -
                                ((item.products.price *
                                    item.products.discount) / 100))).toLocaleString() + ' ₸' }}</small>
                        </div>

                        <div>
                            <span>Дата продажи: {{ formatDate(item.date) }}</span>
                        </div>

                        <div class="buttons">
                            <button @click="createChat(item.buyer.id, item.buyer.user.first_name)">Чат с
                                покупателем</button>
                            <NuxtLink :to="'/product/' + item.products.id">Страница товара</NuxtLink>
                        </div>
                    </div>

                </div>

            </div>
        </div>

        <div class="chats" v-if="activeTab == 3">

            <div class="chat__item" v-for="chat in chats" :key="chat.id">
                <div>
                    <h2>{{ chat.buyer.user.email }}</h2>
                    <!-- <small>23.07.2023 14:47</small> -->
                </div>

                <div class="justify-content-end">
                    <button @click="openChat(chat.id, chat.buyer.user.first_name)">Открыть чат</button>
                </div>
            </div>
        </div>

        <div class="accs" v-if="activeTab == 4">
            <div class="account__profile">
                <div class="profile__left">
                    <div class="avatar w-100">
                        <div class="avik">
                            <label for="fileInput" class="editava ml-0" @click="openFileInput">
                                <span>Изменить фото</span>
                            </label>
                            <input type="file" id="fileInput" ref="fileInput" accept="image/*" style="display: none;"
                                @change="handleFileChange">
                            <!-- Используем avatarUrl для отображения выбранного изображения или дефолтного изображения -->
                            <img :src="avatarUrl" alt="" loading="lazy">
                        </div>
                        <div class="">
                            <label for="name">Отображаемое Имя</label>
                            <input type="text" placeholder="Ваше имя" v-model="name">
                        </div>
                    </div>

                    <div class="data">
                        <label for="name">E-mail</label>
                        <input class="w-100" type="email" placeholder="E-mail" v-model="email">
                    </div>

                    <!-- <div class="data">
                        <label for="name">Пароль</label>
                        <input class="w-100" type="password" placeholder="Пароль">
                    </div> -->

                </div>
                <div class="profile__right w-100">
                    <label for="desc">Описание профиля</label>
                    <textarea name="desc" id="desc" cols="30" rows="17" v-model="description"></textarea>
                </div>
            </div>

            <div class="buttons">
                <button @click="editAccount()" ref="edit">Сохранить изменения</button>
                <button @click="logOut">Выйти из аккаунта</button>
            </div>


        </div>

        <TheTrans v-if="activeTab == 2" :transactions="transactions"></TheTrans>
        <CreateProduct v-if="activeTab == 5"></CreateProduct>
        <EditProduct v-if="activeTab == 6" :productId="sendId"></EditProduct>
        <TheMessanger v-if="activeTab == 7" :chatId="chatId" :name="chatName"></TheMessanger>
    </div>
</template>
<script>
import global from '~/mixins/global';
import axios from 'axios';
export default {
    mixins: [global],
    data() {
        return {
            tabs: ['Мои товары', 'Мои продажи', 'Транзакции', 'Обратная связь', 'Аккаунт'],
            pathUrl: 'https://studynow.kz',
            activeTab: 0,
            tabWidth: 0,
            tabOffset: 0,
            account: [],
            avatar: null,
            name: '',
            email: '',
            description: '',
            photo: '',
            products: [],
            sendId: null,
            chatId: null,
            transactions: [],
            chats: [],
            sales: [],
            myId: null,
        }
    },
    computed: {
        avatarUrl() {
            if (this.avatar) {
                return URL.createObjectURL(this.avatar);
            } else {
                return this.photo;
            }
        },
    },
    methods: {
        openChat(chatId, chatName) {
            this.activeTab = 7;
            this.chatId = chatId;
            this.chatName = chatName
        },
        createChat(id, name) {
            const token = this.getAuthorizationCookie()
            const csrf = this.getCSRFToken()
            const path = `${this.pathUrl}/api/messanger/new-chat`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            axios
                .post(path, {
                    buyer: id,
                    seller: this.myId,
                })
                .then(response => {
                    const chatId = response.data.chat_id
                    this.openChat(chatId, name)
                })
                .catch(error => console.log(error))
        },
        formatDate(dateString) {
            const date = new Date(dateString);
            const formattedDate = `${date.getDate().toString().padStart(2, '0')}.${(date.getMonth() + 1).toString().padStart(2, '0')}.${date.getFullYear()}`;
            return formattedDate;
        },
        openChat(chatId, chatName) {
            this.activeTab = 7;
            this.chatId = chatId;
            this.chatName = chatName
        },
        getChats() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/messanger/all-chats`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;

            axios
                .get(path)
                .then(response => {
                    this.chats = response.data
                })
                .catch(error => {
                    console.log(error)
                })
        },
        openFileInput() {
            this.$refs.fileInput.click();
        },
        handleFileChange(event) {
            const file = event.target.files[0];
            if (file) {
                this.avatar = file;
                event.target.value = null;
                console.log("Выбран файл:", file);
            }
        },
        openEditTab(productId) {
            this.activeTab = 6;
            this.sendId = productId;
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
        getAccount() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/seller/seller-lk`;
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios
                .get(path)
                .then(response => {
                    this.account = response.data
                    this.name = response.data.user.first_name
                    this.email = response.data.user.email
                    this.description = response.data.description
                    this.photo = this.pathUrl + '/api' + response.data.photo
                    this.sales = response.data.my_sales
                    this.products = response.data.products
                    this.transactions = response.data.transactions
                    this.myId = response.data.id

                })
                .catch(error => console.log(error));
        },
        editAccount() {

            const path = `${this.pathUrl}/api/seller/seller-lk/edit/`
            const csrf = this.getCSRFToken()

            const formData = new FormData();
            formData.append('user.[first_name]', this.name);
            formData.append('user.[email]', this.email);

            formData.append('description', this.description);
            if (this.avatar == null) {
                formData.append('photo', '');
            }
            else {
                formData.append('photo', this.avatar);
            }

            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            this.$refs.edit.innerHTML = 'Сохраняем'

            axios
                .put(path, formData)
                .then((res) => {
                    //   console.log('Отправленные данные:', JSON.stringify(res.config.data, null, 2));
                    if (res.status == 200) {
                        this.$refs.edit.innerHTML = 'Успешно'
                        this.name = res.data.user.first_name
                        this.description = res.data.description
                        this.email = res.data.user.email
                    }
                    else {
                        this.$refs.edit.innerHTML = 'Ошибка'
                    }
                })
                .catch((error) => {
                    console.error(error);

                });
        },

    }
    ,
    mounted() {
        this.updateHighlightPosition(this.activeTab);
        const accType = localStorage.getItem('accountType')
        console.log(accType)
        if (accType == 'seller-account') {
            this.getAccount()
            this.getChats()
        }
        else {
            window.location.href = '/login'
        }
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

    .accs {
        .buttons {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 20px;
            margin-top: 30px;

            @media (max-width: 1024px) {
                flex-direction: column;
                align-items: flex-start;

            }

            button,
            a {
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

                @media (max-width: 1024px) {
                    flex: 1;
                }
            }
        }
    }

    .account__profile {
        margin-top: 38px;
        display: flex;
        gap: 20px;

        @media (max-width: 1024px) {
            flex-direction: column;
            margin-top: 20px;
        }

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

            @media (max-width: 1024px) {
                width: 100%;
                max-width: 100%;
                display: inline;
            }
        }


        .profile__left {
            //   width: 100%;

            .data {
                margin-top: 20px;
            }

            .avatar {
                display: flex;
                gap: 20px;
                align-items: start;

                @media (max-width: 1024px) {
                    flex-direction: column;
                    align-items: center;
                    width: 100%;
                }

                .avik {
                    border-radius: 50%;
                }

                img {
                    width: 8.906vw;
                    height: 8.906vw;
                    object-fit: cover;

                    @media (max-width: 1024px) {
                        width: 150px;
                        height: 150px;
                    }
                }

                div {
                    position: relative;
                    overflow: hidden;

                    &:last-child {
                        @media (max-width: 1024px) {
                            width: 100%;
                        }
                    }



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

        @media (max-width: 1400px) {
            gap: 20px;
        }

        @media (max-width: 1024px) {
            margin-top: 20px;
        }

        .chat__item {
            border-radius: 10px;
            background: #FFF;
            box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
            padding: 30px 20px;
            width: 546px;

            @media (max-width: 1024px) {
                width: 100%;
                padding: 15px;
            }

            div {
                display: flex;
                justify-content: space-between;
                align-items: center;
                width: 100%;

                @media (max-width: 380px) {
                    flex-direction: column;
                    align-items: flex-start;
                    gap: 10px;
                }

                h2 {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: normal;
                    font-family: var(--int);
                    color: #000;
                    margin: 0;

                    @media(max-width: 1024px) {
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

                    @media(max-width: 1024px) {
                        font-size: 16px;
                    }
                }
            }

            .justify-content-end {
                justify-content: flex-start !important;
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

        @media (max-width: 1024px) {
            margin-top: 20px;
        }

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

                &:last-child {
                    margin-bottom: 0;
                }

                small {
                    @media (max-width: 1024px) {
                        &:first-child {
                            display: none;
                        }

                    }
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

                        button,
                        a {
                            // flex: 1;
                            padding: 10px 30px;
                            text-align: center;

                            @media (max-width: 1024px) {

                                flex: 1;
                                padding: 10px 0;
                            }
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

        button,
        a {
            padding: 10px 30px;
            border-radius: 10px;
            background: #000;
            border: 0;
            margin-bottom: 34px;
            text-decoration: none;

            font-size: 16px;
            font-style: normal;
            font-weight: 400;
            line-height: 130%;
            color: #fff;

            @media (max-width: 1024px) {
                margin-bottom: 20px;
            }

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
    }
}
</style>