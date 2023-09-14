<template>
    <div class="register w-100">
        <div class="register__left">
            <div class="nex">
                <h1>Регистрация</h1>
                <input type="email" placeholder="Эл.почта" v-model="email" ref="email">
                <input type="password" placeholder="Пароль" v-model="password" ref="password">
                <input type="password" placeholder="Повторите пароль" v-model="repeat__password" ref="repeat__password">
                <input type="text" placeholder="Отображаемое имя" v-model="name" ref="name">

                <div class="buttons">
                    <button :class="{ active: userType == 'buyer' }" @click="userType = 'buyer'">
                        Покупатель
                    </button>
                    <button :class="{ active: userType == 'seller' }" @click="userType = 'seller'">
                        Продавец
                    </button>

                </div>


                <label class="custom-checkbox">
                    <input type="checkbox" v-model="checked">
                    <p class="checkbox-text m-0" ref="checked">Принимаю условия <NuxtLink to='/terms'>
                            Пользовательского
                            соглашения
                        </NuxtLink> и
                        <NuxtLink to='/polytics'>Политики конфиденциальности</NuxtLink>

                    </p>
                </label>



                <div class="text-center">
                    <small>{{ error }}</small>
                    <button @click="register()">Зарегистироваться</button>

                    <span>Уже есть аккаунт? <NuxtLink to='/login'>Вход</NuxtLink></span>
                </div>
            </div>
        </div>
        <div class=" register__right">
            <img src="@/assets/img/loginphoto.png" class="img-fluid" alt="" loading="lazy">
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
            email: '',
            password: '',
            repeat__password: '',
            name: '',
            checked: false,
            error: '',
            userType: 'seller',
            pathUrl: 'https://studynow.kz',
        }
    },
    methods: {
        register() {
            const buyer = `${this.pathUrl}/api/main/registration/buyer`
            const seller = `${this.pathUrl}/api/main/registration/seller`
            const csrf = this.getCSRFToken()

            if (this.email !== '') {
                this.error = ''
                this.$refs.email.style.borderColor = '#000'

                if (this.password != 0 && this.password == this.repeat__password) {
                    this.$refs.password.style.borderColor = '#000'
                    this.$refs.repeat__password.style.borderColor = '#000'
                    this.error = ''

                    if (this.checked) {
                        this.$refs.checked.style.color = '#000'
                        if (this.name !== '') {
                            if (this.userType == 'seller') {

                                this.$refs.name.style.borderColor = '#000'
                                this.error = ''
                                axios.defaults.headers.common['X-CSRFToken'] = csrf;
                                axios
                                    .post(seller, { first_name: this.name, password: this.password, username: this.email, email: this.email })
                                    .then((res) => {

                                        document.cookie = `Authorization=${res.data.token}; expires=Fri, 31 Dec 2023 23:59:59 GMT; path=/`;
                                        console.log(res)
                                        localStorage.setItem('accountType', res.data.redirect_url)
                                        window.location.href = res.data.redirect_url
                                    })
                                    .catch((error) => {
                                        this.error = error.response.data.detail
                                        console.log(error.response);
                                    });

                            }
                            else {
                                axios.defaults.headers.common['X-CSRFToken'] = csrf;
                                this.error = ''
                                axios
                                    .post(buyer, { first_name: this.name, email: this.email, password: this.password, username: this.email, email: this.email })
                                    .then((res) => {

                                        document.cookie = `Authorization=${res.data.token}; expires=Fri, 31 Dec 2023 23:59:59 GMT; path=/`;
                                        console.log(res)
                                        localStorage.setItem('accountType', res.data.redirect_url)
                                        window.location.href = '/'
                                    })
                                    .catch((error) => {
                                        console.log(error.responseS);
                                        this.error = error.response.data.detail
                                    });
                            }
                        }
                        else {
                            this.error = 'Вы не заполнили имя'
                            this.$refs.name.style.borderColor = 'red'
                        }
                    }
                    else {
                        this.$refs.checked.style.color = 'red'
                        this.error = 'Вы не согласились с условиями'
                    }
                }
                else {
                    this.error = 'Пароли не совпадают'
                    this.$refs.password.style.borderColor = 'red'
                    this.$refs.repeat__password.style.borderColor = 'red'
                }
            }
            else {
                this.error = 'Вы не указали почту'
                this.$refs.email.style.borderColor = 'red'
            }
        }
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Регистрация | Studynow',
    ogTitle: 'Регистрация | Studynow',
    description: 'Регистрация | Studynow',
    ogDescription: 'Регистрация | Studynow',
})
</script>
<style lang="scss" scoped>
.register {
    display: flex;

    @media (max-width: 1024px) {
        flex-direction: column-reverse;
        justify-content: center;
    }

    .register__left {
        background: #fff;
        box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
        padding: 0 80px;
        height: 100vh;

        @media (max-width: 1600px) {
            padding: 50px;
        }

        .nex {
            width: 100%;
        }

        @media (max-width: 1024px) {
            background: transparent;
            box-shadow: none;
            justify-content: center;
            padding: 45px 20px;
            align-items: flex-start;
        }

        display: flex;
        align-items: center;

        small {
            //  margin-bottom: 20px;
            text-align: left !important;
            display: block;
            color: red;
            font-family: var(--int);
            font-size: 14px;
        }

        input {
            display: block;
            margin-bottom: 30px;
            width: 100%;
            border: 2px solid #000;
            border-radius: 10px;
            padding: 10px 16px;

            font-size: 16px;
            font-style: normal;
            font-weight: 500;
            line-height: 130%;
            font-family: var(--int);
            color: #3C3C3C;
        }

        h1 {
            font-size: 64px;
            font-style: normal;
            font-weight: 500;
            line-height: 130%;
            font-family: var(--int);
            color: #000;
            margin-bottom: 40px;

            @media (max-width: 1024px) {
                text-align: center;
                font-size: 40px;
                margin-bottom: 20px;
            }
        }

        .text-center {
            button {
                padding: 12px 77px;
                background: #000;
                border: 0;
                border-radius: 10px;
                margin-top: 20px;

                color: #fff;
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);

                &:hover {
                    background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
                }
            }

            span {
                display: block;
                margin-top: 20px;
                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 110%;
                font-family: var(--int);
                color: #000;

                a {
                    color: #000;
                    text-decoration: underline;
                }
            }
        }

        .active {
            background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%) !important;
        }

        .buttons {
            display: flex;
            gap: 29px;
            margin-bottom: 20px;

            button {
                flex: 1;
                border-radius: 10px;
                background: #000;
                padding: 12px 0;
                border: 0;

                color: #fff;
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);

                &:hover {
                    background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
                }
            }
        }
    }

    .register__right {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100%;

        @media (max-width: 1024px) {
            padding: 50px 20px 0;
        }

        img {
            @media (max-width: 1024px) {
                max-width: 236px;
                max-width: 289px;
            }
        }
    }
}

.custom-checkbox p,
.custom-checkbox a {
    font-family: var(--int);
    font-size: 16px;
    font-style: normal;
    font-weight: 400;
    line-height: 130%;
    color: #000;
    max-width: 409px;
    z-index: 50;
}

.custom-checkbox a {
    text-decoration: underline;
}

.custom-checkbox input[type="checkbox"] {
    opacity: 0;
    position: absolute;
    border-radius: 3px;
    z-index: 40;
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
    z-index: 40;
}

.custom-checkbox input[type="checkbox"]:checked+.checkbox-text:before {
    content: url('@/assets/img/check.svg');
    font-size: 16px;
    color: black;
    text-align: center;
    line-height: 20px;
    background: transparent;
    z-index: 40;
}

.custom-checkbox {
    margin-bottom: 22px;
    z-index: 40;
}

.custom-checkbox:last-child {
    margin-bottom: 0 !important;
    z-index: 40;
}
</style>