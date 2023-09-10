<template>
    <div class="complete">
        <prevPage />

        <h1>Корзина</h1>

        <div class="complete__body">
            <div class="cart">
                <div class="cart__item">
                    <img src="@/assets/img/cart2.png" alt="" loading="lazy">

                    <div>
                        <h2>Курс «Блюда высокой кухни со всех стран»</h2>
                        <h2>50 490 ₸</h2>
                        <div class="text-right">
                            <img src="@/assets/img/trashbig.svg" alt="" style="cursor: pointer;">
                        </div>
                    </div>
                </div>
                <div class="cart__item">
                    <img src="@/assets/img/cart2.png" alt="" loading="lazy">

                    <div>
                        <h2>Курс «Блюда высокой кухни со всех стран»</h2>
                        <h3>
                            15 000 ₸
                            <img src="@/assets/img/disc.svg" alt="">
                        </h3>
                        <h2>13 000 ₸</h2>
                        <div class="text-right">
                            <img src="@/assets/img/trashbig.svg" alt="" style="cursor: pointer;">
                        </div>
                    </div>
                </div>

                <div class="cart__item">
                    <img src="@/assets/img/cart2.png" alt="" loading="lazy">

                    <div>
                        <h2>Курс «Блюда высокой кухни со всех стран»</h2>
                        <h2>50 490 ₸</h2>
                        <div class="text-right">
                            <img src="@/assets/img/trashbig.svg" alt="" style="cursor: pointer;">
                        </div>
                    </div>
                </div>
            </div>

            <div class="complete__block">
                <h1>Подтверждение покупки</h1>

                <h2>Количество курсов: 3</h2>
                <h2>Итоговая сумма: 84 080 ₸ </h2>

                <p>Сумма будет списана с вашего счета. Товары отобразятся во вкладке «Мои покупки» в Вашем Личном кабинете.
                </p>

                <div class="text-center">
                    <button>Подтвердить покупку</button>
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
    title: 'Подтверждение покупки | Studynow',
    ogTitle: 'Подтверждение покупки | Studynow',
    description: 'Подтверждение покупки | Studynow',
    ogDescription: 'Подтверждение покупки | Studynow',
})
</script>
<style lang="scss" scoped>
.complete {
    padding: 120px 110px 150px;



    .complete__body {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;

        .complete__block {
            border-radius: 10px;
            background: var(--White, #FFF);
            box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
            padding: 20px 40px 34px;

            h1 {
                text-align: center;
                font-size: 32px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                margin-bottom: 40px;
            }

            h2 {
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
                margin-bottom: 20px;
            }

            p {
                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
                margin-bottom: 40px;
                max-width: 520px;
            }

            button {
                padding: 12px 66px;
                background: #000;
                border-radius: 10px;
                border: 0;

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
        }

        .cart {
            display: flex;
            flex-direction: column;
            gap: 50px;
        }

        .cart__item {
            display: flex;
            gap: 30px;

            img {
                max-width: 220px;
                max-height: 144px;
            }

            div {
                h2 {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #000;
                    margin-bottom: 10px;


                }

                h3 {
                    font-size: 16px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #000;
                    position: relative;
                    margin-bottom: 13px;

                    img {
                        position: absolute;
                        left: 0;
                    }
                }

                h2:nth-child(2) {
                    margin: 0;
                }
            }

        }
    }

    h1 {
        font-size: 40px;
        font-style: normal;
        font-weight: 500;
        line-height: 130%;
        font-family: var(--int);
        color: #000;
        margin-bottom: 30px;
        margin-top: 10px;
    }
}
</style>