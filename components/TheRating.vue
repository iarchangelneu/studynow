<template>
    <div class="star-rating">
        <img v-for="n in maxStars" :key="n" :src="starSrc(n)" :class="{ 'active': n <= rating }">
    </div>
</template>

<script>
export default {
    name: "StarRating",
    props: {
        rating: {
            type: Number,
            required: true
        },
        maxStars: {
            type: Number,
            default: 5
        }
    },
    methods: {
        starSrc(n) {
            if (n <= this.rating) {
                return '/img/yellow_star.svg';
            } else {
                return '/img/grey_star.svg';
            }
        }
    }
};
</script>

<style scoped>
.star-rating {
    display: inline-flex;
    align-items: center;
}

.star-rating img {
    width: 24px;
    height: 24px;
    margin-right: 8px;
}

.star-rating img:last-child {
    margin-right: 0;
}

.star-rating img.active {
    filter: opacity(1);
}
</style>
