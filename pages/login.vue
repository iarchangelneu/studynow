<template>
    <div class="login w-100">
        <div class="login__left">
            <div class="nex">
                <h1>Авторизация</h1>
                <input type="email" placeholder="Эл.почта" v-model="email">
                <input type="password" placeholder="Пароль" v-model="password">

                <div class="text-center">
                    <small>{{ error }}</small>
                    <button @click="login()">Войти</button>

                    <span>Еще нет аккаунта? <NuxtLink to='/register'>Регистрация</NuxtLink></span>
                </div>
            </div>
        </div>
        <div class="login__right">
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
            pathUrl: 'https://studynow.kz',
            error: '',
        }
    },
    methods: {
        login() {
            const path = `${this.pathUrl}/api/main/authorization`
            const csrf = this.getCSRFToken()

            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            axios
                .post(path, { username: this.email, password: this.password })
                .then((res) => {



                    document.cookie = `Authorization=${res.data.token}; expires=Fri, 31 Dec 2023 23:59:59 GMT; path=/`;
                    localStorage.setItem('accountType', res.data.redirect_url)
                    if (res.data.redirect_url == 'buyer-account') {
                        window.location.href = '/'
                    }
                    if (res.data.redirect_url == 'seller-account') {
                        window.location.href = '/seller-account'
                    }


                    console.log(res)
                })
                .catch((error) => {
                    console.log(error);
                    this.error = error.response.data.non_field_errors.toString()
                });
        }
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Авторизация | Studynow',
    ogTitle: 'Авторизация | Studynow',
    description: 'Авторизация | Studynow',
    ogDescription: 'Авторизация | Studynow',
})
</script>
<style lang="scss" scoped>
.login {
    display: flex;

    @media (max-width: 1024px) {
        flex-direction: column-reverse;
        justify-content: center;
    }

    .login__left {
        background: #fff;
        box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
        padding: 0 80px;
        height: 100vh;

        display: flex;
        align-items: center;

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

    .login__right {
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