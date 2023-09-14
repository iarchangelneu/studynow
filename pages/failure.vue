<template>
    <div class="success">
        <div>
            <div class="text">
                <h1>Ошибка транзакции</h1>

            </div>

            <div class="text-center">
                <NuxtLink to="/withdrawal">Попробовать еще раз</NuxtLink>
            </div>

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
            pathUrl: 'https://studynow.kz',
        }
    }
    ,
    methods: {
        sendRequest(reference) {
            const token = this.getAuthorizationCookie();
            const path = `${this.pathUrl}/api/money/failure/${reference}`;
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios
                .get(path)
                .then(response => {
                    console.log(response)
                    if (response.status == 200) {
                        //  window.location.href = '/'
                    }
                })
                .catch(error => {
                    console.log(error);
                });
        },
    },
    mounted() {
        const url = window.location.href;
        const match = url.match(/order_pay_studynow_(\d+)/);

        if (match) {
            this.extractedValue = match[0];
            console.log(this.extractedValue);

            this.sendRequest(match[0])
        }
    },
}
</script>
<script setup>
useSeoMeta({
    title: 'Неудача | Studynow',
    ogTitle: 'Неудача | Studynow',
    description: 'Неудача | Studynow',
    ogDescription: 'Неудача | Studynow',
})
</script>
<style lang="scss" scoped>
.success {
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;

    div {
        .text {
            display: flex;
            align-items: center;
            gap: 15px;

            h1 {
                font-size: 24px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
                margin: 0;

                @media (max-width: 1024px) {
                    font-size: 16px;
                }
            }
        }

        .text-center {
            a {
                display: inline-block;
                padding: 10px 30px;
                border: 0;
                border-radius: 10px;
                background: #000;
                margin-top: 70px;
                text-decoration: none;

                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--int);
                color: #fff;

                @media (max-width: 1024px) {
                    margin-top: 30px;
                }

                &:hover {
                    background: linear-gradient(90deg, #462885 0.64%, #A021A7 100%);
                }
            }
        }
    }
}
</style>