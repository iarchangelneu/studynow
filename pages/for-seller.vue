<template>
    <div class="about">
        <h1>
            Для продавца
        </h1>

        <div class="about__block">
            <div class="about__left">
                <p>
                    Добро пожаловать на платформу для продавцов курсов!
                </p>
                <p> Мы - ваш надежный партнер в создании, продаже и распространении увлекательных онлайн-курсов. Наша
                    платформа предоставляет вам все необходимые инструменты и ресурсы, чтобы превратить ваше знание и опыт в
                    доходное и влиятельное образовательное предприятие.
                </p>

                <h2>Что мы предлагаем:</h2>

                <ol>
                    <li>Простой процесс создания курса: с помощью нашей интуитивно понятной платформы вы можете легко
                        создавать и структурировать свой курс. Добавьте видеоуроки, материалы, тесты и задания, чтобы
                        сделать обучение максимально интерактивным.</li>
                    <li>Мощные инструменты управления: мы предоставляем вам удобные инструменты для управления курсами,
                        учениками и продажами. Отслеживайте свой успех, адаптируйте контент и следите за ростом своей
                        аудитории</li>
                    <li>Персонализированная визуализация: сделайте свой курс узнаваемым и уникальным. Выбирайте собственный
                        дизайн, логотип, цветовую гамму и стиль, чтобы создать брендированное пространство обучения.</li>
                    <li>Гибкая ценовая политика: у вас есть полный контроль над ценой своих курсов. Вы можете определить
                        стоимость самостоятельно и использовать разные модели оплаты, такие как одноразовая покупка,
                        подписка или распродажи.</li>
                    <li>Мгновенный доступ: ваши ученики получают мгновенный доступ к курсам после оплаты. Это обеспечивает
                        легкость и удобство для пользователей, что способствует привлечению и удержанию аудитории.</li>
                    <li>Поддержка и развитие: наша команда поддержки всегда готова помочь вам с вопросами и запросами. Мы
                        также постоянно развиваем платформу, чтобы предоставить вам новые инструменты и функциональность.
                    </li>
                </ol>

                <p>Присоединяйтесь к нам и давайте вместе сделаем ваше знание ценным активом, который поможет другим
                    развиваться и достигать своих целей!</p>

                <div class="text-right">
                    <NuxtLink to="/register">Зарегистироваться</NuxtLink>
                </div>
            </div>

            <div class="about__right">
                <img src="@/assets/img/about1.png" alt="" loading="lazy">

                <div>
                    <img src="@/assets/img/about2.png" alt="" loading="lazy">
                    <img src="@/assets/img/about3.png" alt="" loading="lazy">
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {}
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Для продавца | Studynow',
    ogTitle: 'Для продавца | Studynow',
    description: 'Для продавца | Studynow',
    ogDescription: 'Для продавца | Studynow',
})
</script>
<style lang="scss" scoped>
.about {
    padding: 125px 110px 110px;

    h1 {
        font-size: 40px;
        font-style: normal;
        font-weight: 500;
        line-height: 130%;
        font-family: var(--int);
        color: #000;
        margin-bottom: 30px;
    }

    .about__block {
        display: flex;
        gap: 80px;

        .about__right {
            div {
                margin-top: 40px;
                display: flex;
                gap: 40px;
            }
        }

        .about__left {

            a {
                text-decoration: none;
                padding: 10px 15px;
                border-radius: 10px;
                background: #000;
                display: inline-block;
                margin-top: 0;

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

            p,
            li {
                margin-bottom: 10px;
                max-width: 700px;
                font-size: 20px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
            }



            h2 {
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
                margin-top: 20px;
            }

            ol {
                margin-top: 10px;
                padding-left: 20px;
            }
        }
    }
}
</style>