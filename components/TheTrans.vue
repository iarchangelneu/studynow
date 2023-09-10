<template>
    <div class="transactions text-center">
        <table class="table table-borderless">
            <thead>
                <tr>
                    <th scope="col">Тип</th>
                    <th scope="col">Цена</th>
                    <th scope="col">Дата</th>
                    <th scope="col">Статус</th>
                    <th scope="col">Состояние счета</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>Продажа</td>
                    <td>+ 8 000 ₸</td>
                    <td>05.12.22 15:47</td>
                    <td class="success">Совершено</td>
                    <td>18 000 ₸</td>
                </tr>
                <tr>
                    <td>Продажа</td>
                    <td>+ 8 000 ₸</td>
                    <td>05.12.22 15:47</td>
                    <td class="failure">Отменено</td>
                    <td>18 000 ₸</td>
                </tr>

            </tbody>
        </table>
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
    title: 'Транзакции | Studynow',
    ogTitle: 'Транзакции | Studynow',
    description: 'Транзакции | Studynow',
    ogDescription: 'Транзакции | Studynow',
})
</script>
<style lang="scss" scoped>
.transactions {
    margin-top: 38px;

    table {

        th {
            font-size: 20px;
            font-style: normal;
            font-weight: 500;
            line-height: normal;
            font-family: var(--int);
            color: #000;
            opacity: 0.5;
        }

        td {
            font-size: 24px;
            font-style: normal;
            font-weight: 400;
            line-height: normal;
            font-family: var(--int);
            color: #000;


        }

        .success {
            color: #03B820 !important;
        }

        .failure {
            color: #EA0505 !important;
        }
    }


}
</style>