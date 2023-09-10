<template>
    <div class="catalog">
        <h1>Каталог</h1>

        <div class="catalog__search">
            <div class="input-group">

                <input type="text" class="form-control" placeholder="Поиск курса" aria-label="Поиск курса"
                    aria-describedby="basic-addon1">
                <div class="input-group-prepend">
                    <span class="input-group-text" id="basic-addon1"><img src="@/assets/img/search.svg" alt=""
                            loading="lazy"></span>
                </div>
            </div>

            <div class="filters">
                <button @click="filters = !filters">
                    <span>Фильтр</span>
                    <img src="@/assets/img/filtersarrow.svg" alt="" loading="lazy">
                </button>
                <button @click="sort = !sort">
                    <span>Сортировать</span>
                    <img src="@/assets/img/filtersarrow.svg" alt="" loading="lazy">
                </button>
            </div>
            <div class="sort__body" :class="{ active: sort }">
                <button :class="{ btnactive: selectedSort == 1 }" @click="selectedSort = 1">Сначала дешевле</button>
                <button :class="{ btnactive: selectedSort == 2 }" @click="selectedSort = 2">Сначала дороже</button>
                <button :class="{ btnactive: selectedSort == 3 }" @click="selectedSort = 3">Самые новые</button>
                <button :class="{ btnactive: selectedSort == 4 }" @click="selectedSort = 4">По популярности</button>
            </div>
            <div class="filters__body" :class="{ active: filters }">
                <div>
                    <label class="custom-checkbox">
                        <input type="checkbox">
                        <p class="checkbox-text m-0">IT</p>
                    </label>
                    <label class="custom-checkbox">
                        <input type="checkbox">
                        <p class="checkbox-text m-0">Красота и здоровье</p>
                    </label>
                    <label class="custom-checkbox">
                        <input type="checkbox">
                        <p class="checkbox-text m-0">Творчество и хобби</p>
                    </label>
                    <label class="custom-checkbox">
                        <input type="checkbox">
                        <p class="checkbox-text m-0">Психология</p>
                    </label>
                    <label class="custom-checkbox">
                        <input type="checkbox">
                        <p class="checkbox-text m-0">Языки</p>
                    </label>
                    <label class="custom-checkbox">
                        <input type="checkbox">
                        <p class="checkbox-text m-0">Бизнес</p>
                    </label>
                    <label class="custom-checkbox">
                        <input type="checkbox">
                        <p class="checkbox-text m-0">Спорт</p>
                    </label>
                </div>
                <div>
                    <label class="custom-checkbox">
                        <input type="checkbox">
                        <p class="checkbox-text m-0">Духовное развитие</p>
                    </label>
                    <label class="custom-checkbox">
                        <input type="checkbox">
                        <p class="checkbox-text m-0">Дети</p>
                    </label>
                    <label class="custom-checkbox">
                        <input type="checkbox">
                        <p class="checkbox-text m-0">Маркетинг</p>
                    </label>
                    <label class="custom-checkbox">
                        <input type="checkbox">
                        <p class="checkbox-text m-0">Финансы</p>
                    </label>
                    <label class="custom-checkbox">
                        <input type="checkbox">
                        <p class="checkbox-text m-0">Мода</p>
                    </label>
                    <label class="custom-checkbox">
                        <input type="checkbox">
                        <p class="checkbox-text m-0">Разработка игр</p>
                    </label>
                    <label class="custom-checkbox">
                        <input type="checkbox">
                        <p class="checkbox-text m-0">Продажи</p>
                    </label>
                </div>
                <div>
                    <label class="custom-checkbox">
                        <input type="checkbox">
                        <p class="checkbox-text m-0">Радиотехника</p>
                    </label>
                    <label class="custom-checkbox">
                        <input type="checkbox">
                        <p class="checkbox-text m-0">Бесплатные курсы</p>
                    </label>
                    <label class="custom-checkbox">
                        <input type="checkbox">
                        <p class="checkbox-text m-0">Приготовление пищи</p>
                    </label>
                    <label class="custom-checkbox">
                        <input type="checkbox">
                        <p class="checkbox-text m-0">Съёмка</p>
                    </label>


                    <h2>Цена</h2>
                    <div class="price">
                        <input type="number" placeholder="от">
                        <img src="@/assets/img/line.svg" alt="" loading="lazy">
                        <input type="number" placeholder="до">
                    </div>
                </div>
            </div>
        </div>


        <div class="catalog__body">
            <div class="catalog__item">
                <img src="@/assets/img/sales1.png" />
                <h2>Курсы визажиста «Make-up с нуля»</h2>
                <p>Погрузись в мир красоты с курсом от профессионалов</p>

                <ul class="dot-list">
                    <li>10 видеоуроков</li>
                    <li>3 эксперта</li>
                    <li>Быстрая обратная связь с разбором ошибок</li>
                </ul>

                <div class="price">
                    <h3>13 000 ₸</h3>
                </div>

                <div class="buttons">
                    <NuxtLink to="/product">
                        Подробнее
                    </NuxtLink>
                    <NuxtLink to="/">
                        Купить
                    </NuxtLink>
                </div>
            </div>
        </div>

        <div class="pag text-center">
            <button ref="showmore" @click="pagination">Показать еще</button>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            sort: false,
            filters: false,
            selectedSort: 0,
        }
    },
    methods: {
        pagination() {
            this.$refs.showmore.innerHTML = 'Подгружаем'
            this.$refs.showmore.innerHTML = 'Больше ничего нет (;'
        }
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Каталог | Studynow',
    ogTitle: 'Каталог | Studynow',
    description: 'Каталог | Studynow',
    ogDescription: 'Каталог | Studynow',
})
</script>
<style lang="scss" scoped>
.catalog {
    padding: 125px 110px 90px;

    h1 {
        font-size: 40px;
        font-style: normal;
        font-weight: 500;
        line-height: 130%;
        font-family: var(--int);
        color: #000;


    }

    .pag {
        margin-top: 50px;

        button {
            padding: 10px 30px;
            border: 0;
            border-radius: 10px;
            background: #000;

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

    }

    .catalog__body {
        margin-top: 62px;
        display: flex;
        flex-wrap: wrap;
        gap: 50px;

        .catalog__item {
            padding: 20px;
            border-radius: 10px;
            background: #fff;
            box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
            max-width: 300px;
            display: flex;
            flex-direction: column;

            h2 {
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
                margin-top: 15px;
                margin-bottom: 10px;
            }

            p {
                margin: 10px 0;
                margin-top: auto !important;
                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
            }


            li {
                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
                color: #3C3C3C;
                margin-bottom: 10px;
                position: relative;
                display: flex;
                align-items: flex-start;
                white-space: normal;
            }

            ul {
                padding: 0;
            }

            .buttons {
                display: flex;
                margin-top: 10px;

                gap: 10px;

                a {
                    padding: 10px 15px;
                    text-align: center;
                    background: #000;
                    border-radius: 10px;
                    border: 0;
                    flex: 1;
                    text-decoration: none;

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

            .dot-list {
                list-style-type: none;

                li::before {
                    content: "";
                    min-width: 10px;
                    min-height: 10px;
                    background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
                    border-radius: 50%;
                    margin-right: 15px;
                    margin-top: 5px;
                }

            }

            .price {
                display: flex;
                align-items: center;
                justify-content: center;
                gap: 0 28px;

                span {
                    font-size: 12px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #000;
                    position: relative;

                    img {
                        position: absolute;
                        left: 0;
                    }
                }

                h3 {
                    font-size: 24px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #000;
                }
            }
        }
    }

    .catalog__search {
        display: flex;
        align-items: flex-start;
        justify-content: flex-start;
        gap: 50px;
        margin-top: 42px;
        position: relative;

        .active {
            transform: scaleX(1) !important;
            opacity: 1 !important;
        }

        .sort__body {
            position: absolute;
            right: 16%;
            margin-top: 80px;
            transition: all .3s ease;
            opacity: 0;
            transform: scaleX(0);
            padding: 23px 10px;
            border-radius: 10px;
            background: #fff;
            box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);

            display: flex;
            flex-direction: column;
            gap: 25px;

            button {
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
                text-align: left;
                transition: all .3s ease;
                padding: 7px 20px;

                background: transparent;
                border: 0;
                border-radius: 5px;
            }
        }

        .btnactive {

            background: #FCF0FF !important;
        }

        .filters__body {
            padding: 30px;
            border-radius: 10px;
            background: #fff;
            box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
            position: absolute;
            right: 16%;
            margin-top: 80px;
            transition: all .3s ease;
            opacity: 0;
            transform: scaleX(0);


            display: flex;
            gap: 75px;

            div {
                display: flex;
                flex-direction: column;

                .price {
                    display: flex;
                    flex-direction: row;
                    gap: 5px;

                    input {
                        border-radius: 10px !important;
                        border: 3px solid #000;
                        padding: 6px 10px;
                        max-width: 140px;

                        font-size: 24px;
                        font-style: normal;
                        font-weight: 400;
                        line-height: 130%;
                        font-family: var(--int);
                    }
                }
            }

            h2 {
                font-size: 24px;
                font-style: normal;
                font-weight: 600;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
                margin-bottom: 20px;
            }
        }

        .input-group {
            max-width: 1000px;
        }

        input {
            border-radius: 10px;
            background: #FFF;
            border: 0;
            padding: 15px 30px;
            border-top-right-radius: 0;
            border-bottom-right-radius: 0;
            height: 56px;
            box-shadow: none;
            max-width: 1000px;

            font-size: 20px;
            font-style: normal;
            font-weight: 400;
            line-height: 130%;
            font-family: var(--int);
            color: #3C3C3C;
        }

        .input-group-text {
            border-radius: 10px;
            background: #FFF;
            border: 0;
            border-top-left-radius: 0;
            border-bottom-left-radius: 0;
        }

        .filters {
            display: flex;
            gap: 0 30px;

            button {
                flex: 1;
                display: flex;
                align-items: center;
                gap: 10px;
                border-radius: 10px;
                background: #FFF;
                box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
                padding: 15px 25px;
                border: 0;

                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
            }
        }
    }
}

.custom-checkbox p {
    font-family: var(--int);
    font-size: 20px;
    font-style: normal;
    font-weight: 500;
    line-height: 130%;
    color: #000;
    white-space: nowrap;
}

.custom-checkbox input[type="checkbox"] {
    opacity: 0;
    position: absolute;
    border-radius: 3px;
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
}

.custom-checkbox input[type="checkbox"]:checked+.checkbox-text:before {
    content: url('@/assets/img/check.svg');
    font-size: 16px;
    color: black;
    text-align: center;
    line-height: 20px;
    background: transparent;
}

.custom-checkbox {
    margin-bottom: 22px;
}

.custom-checkbox:last-child {
    margin-bottom: 0 !important;
}
</style>