<template>
	<swiper
		:slides-per-view="1"
		:space-between="50"
		:modules="modules"
		:pagination="{
			clickable: true,
			dynamicBullets: true,
		}"
		class="main-slider__slider flex"
	>
		<swiper-slide
			v-if="data"
			v-for="(item, index) in data.airline_ratings"
			:key="index"
		>
			<AirlinesSlide :index="index" :apiData="data" />
		</swiper-slide>
	</swiper>
</template>
<script setup>
import { Swiper, SwiperSlide } from "swiper/vue";
import { Pagination } from "swiper/modules";

import "swiper/css";
import "swiper/css/pagination";

const modules = [Pagination];
import AirlinesSlide from "./AirlinesSlide.vue";
import axios from "axios";

const data = ref(null);
const error = ref(null);

axios
	.get("http://85.193.81.44:8085/api/v2/overall_rating")
	.then(response => {
		data.value = response.data;
		console.log(data.value);
	})
	.catch(err => {
		error.value = err;
		console.error("Error fetching data:", err);
	});
</script>
<style scoped>
.main-slider__slider {
	max-width: 1100px;
}
</style>
