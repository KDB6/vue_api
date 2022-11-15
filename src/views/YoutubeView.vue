<template>
	<div>
		<HeaderCont />
		<TitleCont name1="Youtube" name2="Reference API" />

		<section className="cont__youtube">
			<div className="container">
				<div className="youtube__inner">
					<div class="youtube__slider">
						<swiper
							:slidesPerView="3"
							:spaceBetween="30"
							:pagination="{
								clickable: true,
							}"
							:modules="{
								Pagination,
								Autoplay,
							}"
							:className="mySwiper"
							:autoplay="{
								delay: 2500,
								disableOnInteraction: false,
							}"
							class="mySwiper"
						>
							<swiper-slide v-for="slider in sliders" :key="slider.id">
								<li>
									<a
										:href="`https://www.youtube.com/watch?v=${slider.id.videoId}`"
									>
										<img
											:src="`${slider.snippet.thumbnails.medium.url}`"
											:alt="`${slider.snippet.description}`"
										/>
									</a>
								</li>
							</swiper-slide>
						</swiper>
					</div>
					<div class="youtube__search">
						<div className="container">
							<h2>검색하기</h2>
							<input
								type="search"
								id="search"
								placeholder="원하시는 영상을 검색해주세요!"
								v-model="search"
							/>
							<button type="submit">검색</button>
						</div>
					</div>
					<div class="youtube__images">
						<ul>
							<li v-for="youtube in youtubes" :key="youtube.id">
								<a :href="`https://unsplash.com/photos/${youtube.id}`">
									<img
										:src="youtube.snippet.thumbnails.medium.url"
										:alt="youtube.snippet.description"
									/>
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
		const sliders = ref([]);
		const youtubes = ref([]);
		const search = ref('landscape');

		const SearchYoutubes = async () => {
			await fetch(
				`https://youtube.googleapis.com/youtube/v3/search?part=snippet&q=킹타쿠&key=AIzaSyABuOUy0Teh_pPVBd6DOP0sB1mj7EnYhs0&query=${search.value}&maxResults=30&type=video`,
			)
				.then(response => response.json())
				.then(result => {
					console.log(result);
					youtubes.value = result.results;
					search.value = '';
				})
				.catch(error => console.log(error));
		};
		SearchYoutubes();

		const RandomYoutubes = () => {
			fetch(
				'https://youtube.googleapis.com/youtube/v3/search?part=snippet&q=킹타쿠&key=AIzaSyABuOUy0Teh_pPVBd6DOP0sB1mj7EnYhs0&maxResults=30&type=video',
			)
				.then(response => response.json())
				.then(result => sliders.value(result.results))
				.catch(error => console.log(error));
		};
		RandomYoutubes();

		return {
			sliders,
			youtubes,
			search,
			SearchYoutubes,
			RandomYoutubes,
			modules: [Pagination, Autoplay],
		};
	},
};
</script>

<style lang="scss">
.cont__youtube {
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

.youtube__search {
	margin-top: 50px;
	margin-bottom: 100px;

	.container {
		position: relative;
	}

	h2 {
		color: var(--dark);
		font-size: 40px;
		text-indent: -9999px;
		height: 0;
		font-family: var(--font-kor);
	}
	input {
		background: #fff;
		border: 1px solid var(--bg--dark-border);
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
		background: #fff;
		color: var(--dark);
		cursor: pointer;
	}
}

.youtube__inner {
	a {
		color: var(--dark);
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
		height: 100%;
		object-fit: cover;
	}
}

.youtube__tag {
	text-align: center;
	margin-bottom: 30px;

	button {
		font-size: 1vw;
		padding: 5px 10px;
		margin: 0 5px;
		border-radius: 5px;
		cursor: pointer;

		&:nth-child(2),
		&:nth-child(3),
		&:nth-child(4),
		&:nth-child(5),
		&:nth-child(6) {
			font-family: var(--font-kor);
		}
	}
}
</style>
