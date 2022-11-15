<template>
	<div>
		<HeaderCont />
		<TitleCont name1="Unsplash" name2="Reference API" />

		<section className="cont__unsplash">
			<div className="container">
				<div className="unsplash__inner">
					<div class="unsplash__slider">
						<swiper
							:slidesPerView="'auto'"
							:centeredSlides="true"
							:spaceBetween="30"
							:pagination="{
								clickable: true,
							}"
							:modules="{
								Pagination,
								Autoplay,
							}"
							:autoplay="{
								delay: 2500,
								disableOnInteraction: false,
							}"
							class="mySwiper"
						>
							<swiper-slide v-for="splash in sliders" :key="splash.id">
								<li>
									<a :href="`https://unsplash.com/photos/${splash.id}`">
										<img
											:src="`https://unsplash.com/photos/${splash.urls.regular}`"
											:alt="`${splash.title}`"
										/>
									</a>
								</li>
							</swiper-slide>
						</swiper>
					</div>
					<div class="unsplash__search"></div>
					<div class="unsplash__images">
						<ul>
							<li v-for="splash in splashes" :key="splash.id">
								<a href="#">
									<img :src="splash.urls.regular" :alt="splash.id" />
								</a>
							</li>
						</ul>
					</div>
				</div>
			</div>
		</section>

		<ContactCont />
		<FooterCont />
	</div>
</template>

<script>
import HeaderCont from '@/components/HeaderCont.vue';
import FooterCont from '@/components/FooterCont.vue';
import TitleCont from '@/components/TitleCont.vue';
import ContactCont from '@/components/ContactCont.vue';
import { ref } from 'vue';

import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';
import 'swiper/css/pagination';
import { Pagination, Autoplay } from 'swiper';

export default {
	components: {
		HeaderCont,
		FooterCont,
		TitleCont,
		ContactCont,
		Swiper,
		SwiperSlide,
	},

	setup() {
		const splashes = ref([]);
		const sliders = ref([]);
		const search = ref('landscape');

		// const SearchSplashes = (search) => {
		//   fetch(
		//     `https://api.unsplash.com/photos/random?client_id=AhDbLOTnwHGYmo4we_vDUhkIf2MTG3fS9HwGmK1slMg&query=${search.value}=color&count=30`
		//   )
		//   	.then(response => response.json())
		// 	.then(result => {
		// 		console.log(result);
		// 		splashes.value = result.results;
		// 		search.value = '';
		// 	})
		// 	.catch(error => console.log(error));
		// };
		// SearchSplashes();

		const SearchSplashes = async () => {
			await fetch(
				`https://api.unsplash.com/photos/random?client_id=AhDbLOTnwHGYmo4we_vDUhkIf2MTG3fS9HwGmK1slMg&query=${search.value}=color&count=30`,
			)
				.then(response => response.json())
				.then(result => {
					console.log(result);
					splashes.value = result.results;
					search.value = '';
				})
				.catch(error => console.log(error));
		};
		SearchSplashes();

		const RandomSplashes = () => {
			fetch(
				'https://api.unsplash.com/photos/random?client_id=AhDbLOTnwHGYmo4we_vDUhkIf2MTG3fS9HwGmK1slMg&query=color&count=30',
			)
				.then(response => response.json())
				.then(result => sliders.value(result.results))
				.catch(error => console.log(error));
		};
		RandomSplashes();

		return {
			splashes,
			search,
			// SearchSplashes,
			RandomSplashes,
			modules: [Pagination, Autoplay],
		};
	},
};
</script>

<style lang="scss">
.cont__unsplash {
	ul {
		column-count: 4;
		column-gap: 20px;
		width: 100%;
	}

	li {
		margin-bottom: 20px;

		img {
			border-radius: 5px;
		}
	}
}

.unsplash__search {
	margin-top: 50px;
	margin-bottom: 100px;

	.container {
		position: relative;
	}

	h2 {
		color: var(--white);
		font-size: 40px;
		text-indent: -9999px;
		height: 0;
		font-family: var(--font-kor);
	}
	input {
		background: #000;
		border: 1px solid var(--white);
		border-radius: 50px;
		color: var(--white);
		width: 100%;
		padding: 14px 20px;
		font-family: var(--font-kor);
	}
	button {
		position: absolute;
		right: 15px;
		top: 7px;
		width: 40px;
		height: 40px;
		border-radius: 50%;
		border: 0;
		font-family: var(--font-kor);
		font-weight: 400;
		z-index: 1000;
		background: #000;
		color: var(--white);
		cursor: pointer;
	}
}

.unsplash__inner {
	a {
		color: var(--white);
	}

	&ul {
		width: 100%;
		display: flex;

		> li {
			&:nth-child(1),
			&:nth-child(2),
			&:nth-child(3),
			&:nth-child(4),
			&:nth-child(5) {
				display: inline;
			}
		}
	}

	.swiper {
		width: 100%;
		height: 100%;
	}

	.swiper-slide {
		text-align: center;
		font-size: 18px;

		/* Center slide text vertically */
		display: -webkit-box;
		display: -ms-flexbox;
		display: -webkit-flex;
		display: flex;
		-webkit-box-pack: center;
		-ms-flex-pack: center;
		-webkit-justify-content: center;
		justify-content: center;
		-webkit-box-align: center;
		-ms-flex-align: center;
		-webkit-align-items: center;
		align-items: center;
	}

	.swiper-slide img {
		display: block;
		width: 100%;
		height: 500px;
		object-fit: cover;
	}

	.swiper-slide {
		width: 100%;
	}
}

.unsplash__tag {
	text-align: center;
	margin-bottom: 30px;

	button {
		font-size: 1vw;
		padding: 5px 10px;
		margin: 0 5px;
		border-radius: 5px;
		cursor: pointer;
	}
}
</style>
