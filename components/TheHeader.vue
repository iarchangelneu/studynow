<template>
    <header>
        <div class="pcheader">
            <div class="crap">
                <img src="@/assets/img/headerlogo.svg" alt="">

                <div class="headermen">
                    <img src="@/assets/img/cart.svg" alt="">
                    <img src="@/assets/img/cash.svg" alt="">
                    <img src="@/assets/img/acc.svg" alt="">

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
                        <NuxtLink to="/">Каталог</NuxtLink>
                        <NuxtLink to="/">Акции и скидки</NuxtLink>
                        <NuxtLink to="/">Популярное</NuxtLink>
                        <NuxtLink to="/">О платформе</NuxtLink>
                        <NuxtLink to="/">Для продавца</NuxtLink>
                    </div>
                    <div>
                        <NuxtLink to="/">Пользовательское соглашение</NuxtLink>
                        <NuxtLink to="/">Политика конфиденциальности</NuxtLink>
                    </div>
                    <NuxtLink to="/" class="reg">Вход/Регистрация</NuxtLink>
                </div>
            </div>
        </div>
    </header>
</template>
<script>
export default {
    data() {
        return {
            menuOpen: false,
        }
    }
}
</script>
<style lang="scss" scoped>
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