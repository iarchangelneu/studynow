<template>
    <footer v-if="!hideFooterOnPages.includes($route.name)">
        <div class="links">
            <div>
                <NuxtLink to="/about">О платформе</NuxtLink>
                <NuxtLink to="/terms">Пользовательское соглашение</NuxtLink>
            </div>
            <div>
                <NuxtLink to="/for-seller">Для продавца</NuxtLink>
                <NuxtLink to="/polytics">Политика конфиденциальности</NuxtLink>
            </div>
        </div>

        <div class="moblinks">
            <div class="logohere">
                <div>
                    <NuxtLink to="/about">О платформе</NuxtLink>
                    <NuxtLink to="/for-seller">Для продавца</NuxtLink>
                </div>
                <NuxtLink to='/'><img src="@/assets/img/footerlogo.svg" alt="" loading="lazy"></NuxtLink>
            </div>
            <NuxtLink to="/terms">Пользовательское соглашение</NuxtLink>
            <NuxtLink to="/polytics">Политика конфиденциальности</NuxtLink>
        </div>

        <NuxtLink to='/' class="pclog"><img src="@/assets/img/footerlogo.svg" alt="" loading="lazy"></NuxtLink>


        <small>
            ТОО WORK 111, 230440033562, Казахстан, город Астана, район Алматы, улица Қалибек Қуанышбаев, дом 15/2, кв. 111,
            почтовый индекс 010000<br>
            Почта поддержки : support@studynow.kz
        </small>
    </footer>
</template>
<script>
export default {
    data() {
        return {
            hideFooterOnPages: ['login', 'register'],
        }
    }
}
</script>
<style lang="scss" scoped>
footer {
    padding: 0 110px 80px;
    display: flex;
    justify-content: space-between;
    align-items: center;

    .moblinks {
        display: none;
    }

    @media (max-width: 1600px) {
        padding: 0 50px 80px;
    }

    @media (max-width: 1024px) {
        padding: 0 20px 40px;
        flex-direction: column;
        align-items: flex-start;
        gap: 20px;

        .pclog {
            display: none;
        }

        .moblinks {
            display: flex;
            flex-direction: column;
            width: 100%;

            a {
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
                text-decoration: none;
                margin-bottom: 25px;

                &:last-child {
                    margin-bottom: 0;
                }
            }

            .logohere {
                width: 100%;
                display: flex;
                align-items: flex-start;
                justify-content: space-between;
                margin-bottom: 25px;

                div {
                    display: flex;
                    flex-direction: column;
                }
            }
        }
    }

    .links {
        display: flex;
        gap: 25px 80px;
        flex-direction: column;

        @media (max-width: 1024px) {
            display: none;
        }

        div {
            display: flex;
            gap: 25px 80px;
            justify-content: space-around;

            @media (max-width: 1600px) {
                gap: 25px 50px;
            }

            @media (max-width: 1024px) {
                flex-direction: column;
                gap: 20px;
            }

            a {
                text-decoration: none;
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #000;

                @media (max-width: 1600px) {
                    font-size: 16px;
                }
            }
        }
    }

    small {
        font-size: 20px;
        font-style: normal;
        font-weight: 400;
        line-height: 130%;
        font-family: var(--int);
        color: #3C3C3C;
        max-width: 567px;

        @media (max-width: 1600px) {
            font-size: 16px;
        }
    }
}
</style>