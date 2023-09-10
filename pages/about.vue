<template>
    <div class="about">
        <h1>
            О платформе
        </h1>

        <div class="about__block">
            <div class="about__left">
                <p>
                    Добро пожаловать на наш сайт продажи курсов!
                </p>
                <p> Здесь вы найдёте неограниченные возможности для саморазвития и обучения новым навыкам. Наша платформа
                    создана для тех, кто стремится расширить свои горизонты, освоить новые области и по‑новому взглянуть
                    на свой
                    потенциал, а также для тех, кто готов поделиться своими навыками.
                </p>
                <p>
                    Мы верим, что образование — это ключ к личному и профессиональному успеху. Наша платформа создана
                    для того,
                    чтобы обучение стало интересным, доступным и эффективным. Независимо от вашего уровня знаний,
                    у нас есть что‑то, что поможет вам достичь новых высот.
                </p>
                <p>Присоединяйтесь к нам сегодня и начните свой увлекательный путь обучения и саморазвития. Вместе
                    мы создаём
                    лучший образовательный опыт для вас!</p>

                <h2>Что мы предлагаем:</h2>

                <ol>
                    <li>Разнообразие: мы предлагаем широкий спектр курсов по самым разнообразным темам — от бизнеса
                        и технологий
                        до искусства и личностного роста. Независимо от вашей цели, у нас есть подходящий курс для вас.</li>
                    <li>Экспертные преподаватели: наши курсы разработаны опытными экспертами в соответствующих областях.
                        Вы будете учиться у лучших специалистов, которые поделятся своими знаниями и опытом.</li>
                    <li>Гибкий режим обучения: мы понимаем, что каждый человек уникален, и поэтому предлагаем разные форматы
                        обучения: онлайн лекции, видеоматериалы, интерактивные задания и многое другое. Вы можете выбрать
                        формат, который подходит именно вам.</li>
                    <li>Сертификация: после успешного окончания курса вы получите официальный сертификат, подтверждающий
                        ваше
                        новое знание или навык. Это может стать вашим активом при поиске работы или продвижении в карьере.
                    </li>
                    <li>Сообщество обучающихся: вы не будете одиноки в своём обучении. Создатели курсов учитывают обратную
                        связь
                        с учениками.</li>
                </ol>

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
    title: 'О платформе | Studynow',
    ogTitle: 'О платформе | Studynow',
    description: 'О платформе | Studynow',
    ogDescription: 'О платформе | Studynow',
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
                margin-top: 54px;

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

            li {
                margin-bottom: 0;
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