<template>
    <div class="login w-100">
        <div class="login__left">
            <div>
                <h1>Авторизация</h1>
                <input type="email" placeholder="Эл.почта" v-model="email">
                <input type="password" placeholder="Пароль" v-model="password">

                <div class="text-center">
                    <button>Войти</button>

                    <span>Еще нет аккаунта? <NuxtLink to='/register'>Регистрация</NuxtLink></span>
                </div>
            </div>
        </div>
        <div class="login__right">
            <img src="@/assets/img/loginphoto.png" alt="" loading="lazy">
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            email: '',
            password: '',
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

    .login__left {
        background: #fff;
        box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
        padding: 0 80px;
        height: 100vh;

        display: flex;
        align-items: center;

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