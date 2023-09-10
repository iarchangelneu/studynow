<template>
    <header v-if="!hideHeaderOnPages.includes($route.name)">
        <div class="pcheader">
            <div class="crap">
                <NuxtLink to="/">
                    <img src="@/assets/img/headerlogo.svg" alt="" loading="lazy">
                </NuxtLink>

                <div class="headermen">
                    <img src="@/assets/img/cart.svg" alt="" loading="lazy" @click="cartOpen = !cartOpen"
                        style="cursor: pointer;">
                    <NuxtLink to="/refill">
                        <img src="@/assets/img/cash.svg" alt="" loading="lazy">
                    </NuxtLink>
                    <NuxtLink to="/seller-account">
                        <img src="@/assets/img/acc.svg" alt="" loading="lazy">
                    </NuxtLink>

                    <div class="burg">
                        <input id="menu__toggle" class="d-none" type="checkbox" />
                        <label class="menu__btn mt-2" for="menu__toggle" @click="menuOpen = !menuOpen">
                            <span></span>
                        </label>
                    </div>
                </div>
            </div>

            <div class="headermenu" :class="{ open: menuOpen }">
                <div class="menu__body">
                    <div>
                        <NuxtLink to="/catalog">Каталог</NuxtLink>
                        <a href="/#sales">Акции и скидки</a>
                        <a href="/#popular">Популярное</a>
                        <NuxtLink to="/about">О платформе</NuxtLink>
                        <NuxtLink to="/for-seller">Для продавца</NuxtLink>
                    </div>
                    <div>
                        <NuxtLink to="/terms">Пользовательское соглашение</NuxtLink>
                        <NuxtLink to="/polytics">Политика конфиденциальности</NuxtLink>
                    </div>
                    <NuxtLink to="/login" class="reg">Вход/Регистрация</NuxtLink>
                </div>
            </div>
        </div>
    </header>

    <div class="cart" :class="{ cartOpen: cartOpen }">
        <div class="d-flex align-items-center justify-content-between">
            <h2>Корзина</h2>
            <img src="@/assets/img/closecart.svg" @click="cartOpen = !cartOpen" alt="" loading="lazy"
                style="cursor: pointer;">
        </div>

        <div class="cart__body">
            <div class="cart__item">
                <img src="@/assets/img/cart.png" alt="" loading="lazy">
                <h3>Блюда высокой кухни со всех стран</h3>

                <div>
                    <img src="@/assets/img/trash.svg" alt="" loading="lazy" style="cursor: pointer;">

                    <small>11 540 ₸</small>
                </div>
            </div>
            <div class="cart__item">
                <img src="@/assets/img/cart.png" alt="" loading="lazy">
                <h3>Блюда высокой кухни со всех стран</h3>

                <div>
                    <img src="@/assets/img/trash.svg" alt="" loading="lazy" style="cursor: pointer;">

                    <small>11 540 ₸</small>
                </div>
            </div>

            <div class="text-center">
                <NuxtLink to="/complete-buy">Перейти к оформлению</NuxtLink>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            menuOpen: false,
            cartOpen: false,
            hideHeaderOnPages: ['login', 'register'],
        }
    }
}
</script>
<style lang="scss" scoped>
.cartOpen {
    transform: scaleY(1) !important;
    opacity: 1 !important;
}

.cart {
    padding: 60px;
    background: #FFF;

    position: fixed;
    width: 30%;
    z-index: 200;
    right: 0;
    height: 100vh;
    transition: all .3s ease;
    transform: scaleY(0);
    opacity: 0;

    .cart__body {
        margin-top: 75px;

        a {
            margin-top: 40px;
            display: inline-block;
            text-decoration: none;
            text-align: center;
            padding: 12px 57px;
            border-radius: 10px;
            background: #000;

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

        .cart__item {
            display: flex;
            margin-bottom: 20px;

            img {
                max-width: 176px;
                max-height: 122px;
            }

            &:last-child {
                margin-bottom: 0;
            }

            h3 {
                font-size: 14px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
                margin-left: 10px;
                margin-bottom: 0;
            }

            div {
                display: flex;
                flex-direction: column;
                align-items: flex-end;
                gap: 35px;

                small {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: normal;
                    font-family: var(--int);
                    color: #000;
                    white-space: nowrap;
                }
            }
        }
    }

    h2 {
        font-size: 40px;
        font-style: normal;
        font-weight: 500;
        line-height: normal;
        font-family: var(--int);
        color: #000;
    }
}

header {
    z-index: 150;
    display: flex;
    justify-content: center;
    position: fixed;
    padding: 25px 378px 0;
    width: 100%;

    .pcheader {
        width: 100%;
        height: auto;
        border-radius: 15px;
        background: rgba(164, 164, 164, 0.13);
        box-shadow: -40.83333px 40.83333px 40.83333px 0px rgba(255, 255, 255, 0.13) inset, 40.83333px -40.83333px 40.83333px 0px rgba(165, 165, 165, 0.13) inset;
        backdrop-filter: blur(44.91666793823242px);
        padding: 12px 25px;
        position: relative;
        transition: all .3s ease;

        .crap {
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all .3s ease;
        }

        .headermen {
            display: flex;
            align-items: center;
            gap: 0 30px;
            transition: all .3s ease;
        }

        .headermenu {
            position: absolute;
            border-top: 1px solid #CDCDCD;
            margin-top: 12px;
            transition: all .1s ease;
            transform: scaleY(0) !important;
            opacity: 0;
            height: 0;

            .menu__body {
                padding: 30px;
                display: flex;
                justify-content: space-between;
                align-items: flex-start;

                div {
                    display: flex;
                    flex-direction: column;
                    gap: 25px;

                    a {
                        text-decoration: none;
                        font-size: 20px;
                        font-style: normal;
                        font-weight: 400;
                        line-height: 130%;
                        font-family: var(--int);
                        color: #000;
                    }
                }

                .reg {
                    text-decoration: none;
                    display: inline-block;
                    text-align: center;
                    padding: 10px 30px;

                    border-radius: 10px;
                    background: #000;
                    font-size: 16px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #fff;
                    transition: all .3s ease;

                    &:hover {
                        background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
                    }
                }
            }
        }

        .open {
            position: relative;
            transform: scaleY(1) !important;
            opacity: 1;
            height: auto;
        }
    }
}

#menu__toggle {
    opacity: 0;
}

.menu__btn {
    display: flex;
    /* используем flex для центрирования содержимого */
    align-items: center;
    /* центрируем содержимое кнопки */
    width: 35px;
    height: 20px;
    cursor: pointer;
    z-index: 100000000;
    color: #fff;
    position: relative;
    transform: rotate(180deg);
}

.menu__btn>span {
    display: block;
    position: absolute;
    width: 100%;
    height: 2px;
    background-color: #000;
}

.menu__btn>span::before,
.menu__btn>span::after {
    display: block;
    position: absolute;
    width: 100%;
    height: 2px;
    background-color: #000;
}

.menu__btn>span::before {
    content: '';
    top: -8px;
}

.menu__btn>span::after {
    content: '';
    top: 8px;
}

#menu__toggle:checked~.menu__btn>span {
    transform: rotate(45deg);
    background-color: #000;
    border-radius: 10px;

}

#menu__toggle:checked~.menu__btn>span::before {
    top: 0;
    transform: rotate(0);
    background-color: #000;
    border-radius: 10px;

}

#menu__toggle:checked~.menu__btn>span::after {
    top: 0;
    transform: rotate(90deg);
    background-color: #000;
    border-radius: 10px;
}

#menu__toggle:checked~.menu__box {
    visibility: visible;
    top: 0;
}

.menu__btn>span,
.menu__btn>span::before,
.menu__btn>span::after {
    transition-duration: .25s;
}
</style>