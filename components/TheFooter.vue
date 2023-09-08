<template>
    <footer>
        <div class="links">
            <div>
                <NuxtLink to="/">О платформе</NuxtLink>
                <NuxtLink to="/">Пользовательское соглашение</NuxtLink>
            </div>
            <div>
                <NuxtLink to="/">Для продавца</NuxtLink>
                <NuxtLink to="/">Политика конфиденциальности</NuxtLink>
            </div>
        </div>

        <img src="@/assets/img/footerlogo.svg" alt="">


        <small>
            г. Алматы, пр-кт Республики 13, Почтовый индекс A15X3C5 (050013), +7 775 816 82 48, БИН 210840016943
            Почта поддержки : support@studynow.kz
        </small>
    </footer>
</template>
<style lang="scss" scoped>
footer {
    padding: 0 110px 80px;
    display: flex;
    justify-content: space-between;
    align-items: center;

    .links {
        display: flex;
        gap: 25px 80px;
        flex-direction: column;

        div {
            display: flex;
            gap: 25px 80px;
            justify-content: space-around;

            a {
                text-decoration: none;
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
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
    }
}
</style>