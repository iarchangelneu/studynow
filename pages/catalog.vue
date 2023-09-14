<template>
    <div class="catalog">
        <h1>Каталог</h1>

        <div class="catalog__search">
            <div class="input-group">

                <input type="text" class="form-control" placeholder="Поиск курса" aria-label="Поиск курса"
                    aria-describedby="basic-addon1" v-model="search" @input="searchProducts">
                <div class="input-group-prepend">
                    <span class="input-group-text" id="basic-addon1"><img src="@/assets/img/search.svg" alt=""
                            loading="lazy"></span>
                </div>
            </div>

            <div class="filters">
                <button @click="filters = !filters" :class="{ activefilter: filters }">
                    <span>Фильтр</span>
                    <img src="@/assets/img/filtersarrow.svg" alt="" loading="lazy" :class="{ activearrow: filters }">
                </button>
                <button @click="sort = !sort" :class="{ activefilter: sort }">
                    <span>Сортировать</span>
                    <img src="@/assets/img/filtersarrow.svg" alt="" loading="lazy" :class="{ activearrow: sort }">
                </button>
            </div>
            <div class="sort__body" :class="{ active: sort }">
                <button :class="{ btnactive: selectedSort == 1 }" @click="selectedSort = 1, sortBy('price')">Сначала
                    дешевле</button>
                <button :class="{ btnactive: selectedSort == 2 }" @click="selectedSort = 2, sortBy('-price')">Сначала
                    дороже</button>
                <button :class="{ btnactive: selectedSort == 3 }" @click="selectedSort = 3, sortBy('-date_activate')">Самые
                    новые</button>
                <button :class="{ btnactive: selectedSort == 4 }" @click="selectedSort = 4, sortBy('date_activate')">Самые
                    старые</button>
            </div>
            <div class="filters__body" :class="{ active: filters }">
                <div>
                    <label class="custom-checkbox" v-for="(category, index) in categories1" :key="index">
                        <input type="checkbox" :value="index + 1" v-model="selectedCategories" @change="applyFilters">
                        <p class="checkbox-text m-0">{{ category }}</p>
                    </label>

                </div>
                <div>
                    <label class="custom-checkbox" v-for="(category, index) in categories2" :key="index">

                        <input type="checkbox" :value="index + 8" v-model="selectedCategories" @change="applyFilters">
                        <p class="checkbox-text m-0">{{ category }}</p>
                    </label>

                </div>
                <div>
                    <label class="custom-checkbox" v-for="(category, index) in categories3" :key="index">
                        <input type="checkbox" :value="index + 15" v-model="selectedCategories" @change="applyFilters">
                        <p class="checkbox-text m-0">{{ category }}</p>
                    </label>




                    <div class="cas">
                        <h2>Цена</h2>
                        <div class="price">
                            <input type="number" placeholder="от" v-model="minPrice" @input="applyFilters">
                            <img src="@/assets/img/line.svg" alt="" loading="lazy">
                            <input type="number" placeholder="до" v-model="maxPrice" @input="applyFilters">
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div v-if="catalog.length <= 0"></div>
        <div class="catalog__body" v-else>
            <div class="catalog__item" v-for="item in catalog.results" :key="item.id">
                <img :src="pathUrl + '/api' + item.add_image[0]" class="productimg" />
                <h2>{{ item.name }}</h2>
                <p>{{ item.short_description }}</p>

                <ul class="dot-list" v-if="item.key_features">
                    <li v-for="(feature, index) in item.key_features.split('\r\n').slice(0, 3)" :key="index">{{ feature }}
                    </li>
                </ul>

                <div class="price">
                    <span v-if="item.discount > 0">
                        {{ item.price.toLocaleString() + ' ₸' }}
                        <img src="@/assets/img/disc.svg" alt="" loading="lazy">
                    </span>
                    <h3 v-if="item.discount > 0">
                        {{ (Math.floor(item.price - ((item.price * item.discount) / 100))).toLocaleString() + ' ₸' }}</h3>
                    <h3 v-else>{{ item.price == 0 ? 'Бесплатно' : item.price.toLocaleString() + ' ₸' }}</h3>
                </div>

                <div class="buttons">
                    <NuxtLink :to="'/product/' + item.id" ref="buy">
                        Подробнее
                    </NuxtLink>
                    <NuxtLink ref="buy" @click="addToCart(item.id)" style="cursor: pointer;">
                        {{ item.addToCartStatus || 'Купить' }}
                    </NuxtLink>
                </div>
            </div>
        </div>

        <div class="pag text-center">
            <button ref="showmore" @click="loadMoreProducts()">Показать еще</button>
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
            sort: false,
            filters: false,
            selectedSort: 0,
            selectedCategories: [],
            addToCartStatus: '',
            catalog: [],
            minPrice: null,
            maxPrice: null,
            pathUrl: 'https://studynow.kz',
            search: '',
            categories1: ['IT', 'Красота и здоровье', 'Творчество и хобби', 'Психология', 'Языки', 'Бизнес', 'Спорт'],
            categories2: ['Духовное развитие', 'Дети', 'Маркетинг', 'Финансы', 'Мода', 'Разработка игр', 'Продажи'],
            categories3: ['Радиотехника', 'Бесплатные курсы', 'Приготовление пищи', 'Съёмка'],
        }
    },
    methods: {

        addToCart(id) {
            const path = `${this.pathUrl}/api/buyer/add-product-basket`
            const csrf = this.getCSRFToken()
            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            axios
                .post(path, {
                    products: id,
                    amount: 1,
                })
                .then(response => {
                    const index = this.catalog.results.findIndex(item => item.id === id);
                    if (response.status == 201) {
                        // Присвоение значения напрямую
                        this.catalog.results[index].addToCartStatus = 'Добавлен';
                    } else {
                        this.catalog.results[index].addToCartStatus = 'Ошибка';
                    }
                    console.log(response)
                })
                .catch(error => {
                    console.error(error)
                })
        },
        getCatalog() {
            const queryParams = new URLSearchParams(window.location.search);
            const categoryParam = queryParams.get('category');
            const searchParam = queryParams.get('search');



            let url = `${this.pathUrl}/api/products/all-product`;
            if (searchParam) {
                url += `?name__icontains=${searchParam}`;
            }
            if (categoryParam) {
                url += `?category__in=${categoryParam}`;
            }

            axios
                .get(url)
                .then(response => {
                    this.catalog = response.data;
                })
                .catch(error => {
                    console.error(error);
                });
        },
        loadMoreProducts() {
            if (this.catalog.next) {
                this.$refs.showmore.innerHTML = 'Загружаем'
                axios
                    .get(this.catalog.next)
                    .then(response => {
                        // Добавляем новые продукты к существующим
                        this.catalog.results.push(...response.data.results);
                        this.catalog.next = response.data.next;
                    })
                    .catch(error => {
                        console.error(error);
                    });
            }
            else {
                this.$refs.showmore.innerHTML = 'Больше ничего нет (;'
            }
        },
        sortBy(ordering) {
            this.sort = false
            const path = `${this.pathUrl}/api/products/all-product?ordering=${ordering}`;
            axios
                .get(path)
                .then(response => {
                    this.catalog = response.data;

                })
                .catch(error => {
                    console.error(error);
                });
        },

        applyFilters() {
            const params = new URLSearchParams();
            if (this.minPrice !== null) {
                params.append('price__gte', this.minPrice);
            }
            if (this.maxPrice !== null) {
                params.append('price__lte', this.maxPrice);
            }

            if (this.selectedCategories.length > 0) {
                params.append('category__in', this.selectedCategories.join(','));
            }
            if (this.search) {
                params.append('name__icontains', this.search);
            }

            this.fetchFilteredProducts(params);
        },
        fetchFilteredProducts(params) {
            const path = `${this.pathUrl}/api/products/all-product?${params.toString()}`;
            axios
                .get(path)
                .then(response => {
                    this.catalog = response.data;
                })
                .catch(error => {
                    console.error(error);
                });
        },
        searchProducts() {
            const query = this.search.trim();
            if (query) {
                const queryParams = `?name__icontains=${query}`;
                this.fetchSearchResults(queryParams);
            } else {
                this.getCatalog();
            }
        },
        fetchSearchResults(queryParams) {
            const path = `${this.pathUrl}/api/products/all-product${queryParams}`;
            axios
                .get(path)
                .then(response => {
                    this.catalog = response.data;
                })
                .catch(error => {
                    console.error(error);
                });
        },
    },
    mounted() {
        this.getCatalog()
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
.productimg {
    height: 174px;
    width: 100%;
    object-fit: cover;
    border-radius: 10px;

    @media (max-width: 1024px) {
        height: 230px;
    }
}

.catalog {
    padding: 125px 110px 90px;

    @media (max-width: 1660px) {
        padding: 125px 50px 90px;
    }

    @media (max-width: 1024px) {
        padding: 125px 20px 50px;
    }

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
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
        gap: 50px;
        grid-auto-flow: dense;
        margin-top: 30px;

        @media (max-width: 1600px) {
            gap: 40px;
        }

        @media (max-width: 1400px) {
            gap: 20px;
            justify-content: center;
        }

        .catalog__item {
            padding: 20px;
            border-radius: 10px;
            background: #fff;
            box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
            max-width: 100%;
            display: flex;
            flex-direction: column;

            @media (max-width: 1200px) {
                max-width: 100%;
                width: 100%;
                padding: 10px;
            }

            img {
                max-width: 100%;
            }


            h2 {
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
                margin-top: 15px;
                margin-bottom: 10px;

                @media (max-width: 1024px) {
                    font-size: 16px;
                }
            }

            p {
                margin: 10px 0;
                margin-top: auto !important;
                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);

                @media (max-width: 1024px) {
                    font-size: 12px;
                }
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

                @media (max-width: 1024px) {
                    font-size: 12px;
                }
            }

            ul {
                padding: 0;
            }

            .buttons {
                display: flex;
                margin-top: 10px;

                gap: 10px;

                @media (max-width: 1024px) {
                    padding: 0 20px;
                    flex-direction: row-reverse;
                }

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

                @media (max-width: 1024px) {
                    flex-direction: row-reverse;
                }

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

                    @media (max-width: 1024px) {
                        font-size: 20px;
                    }
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

        @media (max-width: 1024px) {
            flex-direction: column;
            gap: 20px;
        }

        .active {
            transform: scaleX(1) !important;
            opacity: 1 !important;

            @media (max-width: 1024px) {
                transform: scaleY(1) !important;
            }
        }

        .sort__body {
            position: absolute;
            right: 0;
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

            @media (max-width: 1024px) {
                margin-top: 150px;
                right: 0;
                gap: 10px;
            }

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
            right: 0;
            margin-top: 80px;
            transition: all .3s ease;
            opacity: 0;
            transform: scaleX(0);
            z-index: 15;


            display: flex;
            gap: 75px;

            @media (max-width: 1024px) {
                flex-direction: column-reverse;
                right: 0;
                margin-top: 150px;
                transform: scaleY(0);
                width: 100%;
                padding: 15px;
                gap: 0px;
            }

            .cas {
                flex-direction: column;
                margin-bottom: 30px;
            }

            div {
                display: flex;
                flex-direction: column;

                @media (max-width: 1024px) {
                    flex-direction: column-reverse;
                }

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

                        @media (max-width: 1024px) {
                            max-width: 120px;
                            padding: 4px 10px;
                        }
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
            width: 100%;

            @media (max-width: 1024px) {
                gap: 20px;
            }

            .activefilter {
                background: #FCF0FF;
            }

            .activearrow {
                transform: rotate(90deg);
            }

            button {
                flex: 1;
                display: flex;
                justify-content: center;
                align-items: center;
                gap: 10px;
                border-radius: 10px;
                background: #FFF;
                box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
                padding: 15px 25px;
                border: 0;
                transition: all .3s ease;

                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #000;

                @media (max-width: 1024px) {
                    font-size: 16px;
                    padding: 15px 20px;
                }

                img {
                    transition: all .3s ease;
                }
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

    @media (max-width: 1024px) {
        margin-bottom: 22px !important;
    }
}
</style>