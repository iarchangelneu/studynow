<template>
    <div>
        <div class="course">
            <div class="course__left">
                <div>
                    <label for="name">Название товара</label>
                    <input type="text" id="name" name="name" placeholder="Введите название" v-model="name">
                </div>
                <div>
                    <label for="name">Краткое описание</label>
                    <input type="text" id="name" name="name" placeholder="Введите краткое описание" v-model="shortDesc">
                </div>

                <div class="select">
                    <div class="mb-0">
                        <label for="select">Выберите категорию</label>
                        <select name="select" id="select" v-model="selectedCategory">
                            <option v-for="(category, index) in categories" :key="index" :value="category.id">{{
                                category.name
                            }}</option>
                        </select>
                    </div>
                    <span v-if="selectedCategory !== null">
                        {{ getCategoryName(selectedCategory) }}
                        <img src="@/assets/img/del.svg" alt="" loading="lazy" @click="clearSelection">
                    </span>
                </div>

                <div class="discount">
                    <div>
                        <label for="name">Введите цену</label>
                        <input type="number" id="name" name="name" placeholder="Цена за товар">
                    </div>
                    <div>
                        <label for="name">Скидка, %</label>
                        <input type="number" id="name" name="name" placeholder="" v-model="discount" @input="limitValue">
                    </div>

                </div>
                <div>
                    <label for="name">Загрузка изображений (до 3)</label>
                    <div class="mb-0 fileupload" @dragover.prevent="highlightDropArea"
                        @dragleave.prevent="unhighlightDropArea" @drop.prevent="handleDrop" @click="openFileInput">
                        <span>{{ alert }}</span>
                        <small>Открыть</small>
                        <input type="file" ref="fileInput" style="display: none" accept="image/*" multiple
                            @change="handleFileInput" />
                    </div>


                    <div class="uploaded-images">
                        <div v-for="(image, index) in uploadedImages" :key="index" class="uploaded-image">
                            <img :src="image.url" alt="Uploaded Image" />
                        </div>
                    </div>
                </div>
            </div>

            <div class="course__right">
                <div>
                    <label for="tabs">Особенности курса (До 6)</label>
                    <div class="custom-textarea">
                        <textarea class="features-list" сols="30" rows="10" ref="featuresList" v-model="courseFeaturesText"
                            @keydown="handleKeyDown"></textarea>
                    </div>
                </div>
                <div>
                    <label for="tabs">Описание товара</label>
                    <textarea name="" id="" cols="30" rows="10" v-model="description">

                </textarea>
                </div>
            </div>
        </div>

        <div class="text-center">
            <button>Опубликовать товар</button>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            selectedCategory: null,
            discount: 0,
            name: '',
            shortDesc: '',
            description: '',
            alert: 'Перетащите файлы сюда или откройте вручную',
            uploadedImages: [],
            courseFeaturesText: '',
            categories: [
                { id: 1, name: "IT" },
                { id: 2, name: "Красота и здоровье" },
                { id: 3, name: "Творчество и хобби" },
                { id: 4, name: "Психология" },
                { id: 5, name: "Духовное развитие" },
                { id: 6, name: "Дети" },
                { id: 7, name: "Маркетинг" },
                { id: 8, name: "Финансы" },
                { id: 9, name: "Радиотехника" },
                { id: 10, name: "Бесплатные курсы" },
                { id: 11, name: "Приготовление пищи" },
                { id: 12, name: "Съёмка" },
                { id: 13, name: "Языки" },
                { id: 14, name: "Бизнес" },
                { id: 15, name: "Спорт" },
                { id: 16, name: "Разработка игр" },
                { id: 17, name: "Продажи" },
                { id: 18, name: "Мода" },
            ],
        }
    },

    methods: {
        handleKeyDown(event) {
            if (event.key === 'Backspace' && !this.courseFeaturesText) {
                event.preventDefault(); // Предотвращаем удаление последней строки
                return;

            }

            const lines = this.courseFeaturesText.split('\n');
            if (lines.length >= 6 && event.key === 'Enter') {
                event.preventDefault();
                this.$refs.featuresList.style.borderColor = 'red' // Предотвращаем Редактирование новой строки после 6 строк
                return;
            }
        },
        getCategoryName(categoryId) {
            const category = this.categories.find((c) => c.id === categoryId);
            return category ? category.name : "";
        },
        clearSelection() {
            this.selectedCategory = null;
        },
        limitValue() {
            if (this.discount > 100) {
                this.discount = 100; // Ограничиваем значение до 100
            }
        },
        highlightDropArea(event) {
            // Подсветить область при перетаскивании
            event.currentTarget.classList.add('highlight');
        },
        unhighlightDropArea(event) {
            // Убрать подсветку области при завершении перетаскивания
            event.currentTarget.classList.remove('highlight');
        },
        handleDrop(event) {
            // Обработать файлы, перетащенные на область
            event.preventDefault();
            this.unhighlightDropArea(event);

            const files = event.dataTransfer.files;
            this.processFiles(files);
        },
        handleFileInput() {
            // Обработать выбранные файлы из инпута
            const files = this.$refs.fileInput.files;
            this.processFiles(files);
        },
        processFiles(files) {
            // Проверить, что загруженные файлы - изображения
            const imageFiles = [];
            for (let i = 0; i < files.length; i++) {
                if (files[i].type.startsWith('image/')) {
                    imageFiles.push(files[i]);
                }
            }

            if (this.uploadedImages.length + imageFiles.length > 3) {
                this.alert = 'Можно загрузить не более 3х изображений'
                return;
            }

            // Создать объекты для загруженных изображений и добавить их в массив
            imageFiles.forEach((file) => {
                const imageUrl = URL.createObjectURL(file);
                this.uploadedImages.push({ url: imageUrl, file });
            });

            // Здесь можно добавить дополнительную логику обработки загруженных изображений
        },
        openFileInput() {
            // Проксировать клик на скрытый input для выбора файлов
            this.$refs.fileInput.click();
        },
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Редактирование курса | Studynow',
    ogTitle: 'Редактирование курса | Studynow',
    description: 'Редактирование курса | Studynow',
    ogDescription: 'Редактирование курса | Studynow',
})
</script>
<style lang="scss" scoped>
.text-center {
    button {
        margin-top: 30px;
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

.course {
    margin-top: 34px;
    display: flex;
    gap: 20px;
    width: 100%;

    label,
    input {
        display: block;
    }

    label {
        margin-left: 10px;
        font-size: 16px;
        font-style: normal;
        font-weight: 500;
        line-height: 110%;
        font-family: var(--int);
        color: #000;
    }

    .uploaded-images {
        display: flex;
        flex-wrap: wrap;
        gap: 9px;
        margin-top: 20px;

        img {
            max-width: 259px;
            max-height: 177px;
        }
    }

    input,
    select {
        background: transparent;
        border: 2px solid #000;
        border-radius: 10px;
        padding: 10px;
        width: 100%;

        font-size: 16px;
        font-style: normal;
        font-weight: 400;
        line-height: 130%;
        font-family: var(--int);
        color: #000;
    }

    .course__left {
        max-width: 527px;

        .highlight {
            border: 2px dashed green !important;
            cursor: pointer;
            /* Добавьте курсор-указатель, чтобы показать, что область можно нажать */
        }

        .fileupload {
            border-radius: 10px;
            border: 2px solid #000;
            padding: 10px;
            display: flex;
            justify-content: space-between;
            cursor: pointer;


            span {
                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
                color: #3C3C3C;
            }

            small {
                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                text-decoration-line: underline;
                font-family: var(--int);
                color: #000;
            }
        }

        width: 100%;

        div {
            margin-bottom: 20px;
            max-width: 527px;

            &:last-child {
                margin-bottom: 0;
            }
        }

        .discount {
            display: flex;
            gap: 10px;
        }

        .select {
            display: flex;
            align-items: flex-end;
            gap: 10px;

            span {
                padding: 11px 10px;
                margin-top: 4px;
                border: 2px solid #000;
                border-radius: 10px;

                display: flex;
                align-items: flex-start;
                gap: 10px;
                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
                color: #000;

                img {
                    cursor: pointer;
                }
            }
        }
    }

    .course__right {
        width: 100%;

        .custom-textarea {
            width: 100%;
            background: transparent;

        }

        .features-list {
            outline: none;
            white-space: pre-wrap;
            width: 100%;
        }

        textarea {
            width: 100%;
            border-radius: 10px;
            border: 2px solid #000;
            background: transparent;
            padding: 20px;
        }

        div {
            margin-bottom: 20px;

            &:last-child {
                margin-bottom: 0;
            }
        }
    }
}
</style>