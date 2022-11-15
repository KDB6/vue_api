<!-- eslint-disable prettier/prettier -->
<!-- <template>
	<div>
		<HeaderCont />
		<TitleCont name1="Unsplash" name2="Reference API" />

		<section className="cont__refer">
			<div className="container">
				<div className="unsplash__inner">
					<div class="unsplash__slider"></div>
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

export default {
	components: {
		HeaderCont,
		FooterCont,
		TitleCont,
		ContactCont,
	},

	setup() {
		const splashes = ref([]);
		const search = ref('landscape');

		// const SearchSplashes = (search) => {
		//   fetch(
		//     `https://api.unsplash.com/search/photos?client_id=AhDbLOTnwHGYmo4we_vDUhkIf2MTG3fS9HwGmK1slMg&query=${search.value}`
		//   )
		//     .then((response) => response.json())
		//     .then((result) => console.log(result))
		//     .catch((error) => console.log(error));
		// };
		// SearchSplashes();

		const RandomSplashes = () => {
			fetch(
				'https://api.unsplash.com/photos/random?client_id=AhDbLOTnwHGYmo4we_vDUhkIf2MTG3fS9HwGmK1slMg=20',
			)
				.then(response => response.json())
				.then(result => splashes.value(result))
				.catch(error => console.log(error));
		};
		RandomSplashes();

		return {
			splashes,
			search,
			// SearchSplashes,
			RandomSplashes,
		};
	},
};
</script> -->

<template>
	<div>
		<HeaderCont />
		<TitleCont name1="Unsplash" name2="reference API" />
		<section class="cont__unspalsh">
			<div class="container">
				<div class="unspalsh__inner">
					<div class="unspalsh__slider">
						<swiper
							:slidesPerView="'auto'"
							:centeredSlides="true"
							spaceBetween="30"
							pagination={{
								clickable: true,
							}}
							modules="{[Pagination, Autoplay]}"
							class="mySwiper"
							autoplay={{
								delay: 2500,
								disableOnInteraction: false,
							}};
						>
							<swiper-slide v-for="slider in sliders" :key="slider.id">
								<li>
									<a :href="`https://www.themoviedb.org/movie/${slider.id}`">
										<img
											:src="`https://image.tmdb.org/t/p/w500/${slider.poster_path}`"
											:alt="`${slider.title}`"
										/>
										<em>
											<span className="title">{{ slider.title }}</span>
											<span className="score">{{ slider.vote_average }}</span>
										</em>
									</a>
								</li>
							</swiper-slide>
						</swiper>
					</div>
					<div class="movie__search">
						<div class="container">
							<h2>검색하기</h2>
							<form @submit.prevent="SearchMovies()">
								<input
									type="search"
									id="search"
									placeholder="원하시는 영화를 검색해주세요!"
									v-model="search"
								/>
								<button type="submit">검색</button>
							</form>
						</div>
					</div>
					<div class="movie__movies">
						<div class="container">
							<div class="movie__list">
								<ul>
									<li v-for="movie in movies" :key="movie.id">
										<a :href="`https://image.tmdb.org/movie/${movie.id}`">
											<img
												:src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
												:alt="movie.title"
											/>
										</a>
									</li>
								</ul>
							</div>
						</div>
					</div>
					<!-- //movie__movies -->
				</div>
			</div>
		</section>
		<FooterCont />
		<ContactCont />
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
import 'swiper/css/effect-coverflow';
import 'swiper/css/pagination';
import { EffectCoverflow, Pagination, Autoplay } from 'swiper';

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
		const movies = ref([]);
		const sliders = ref([]);
		const search = ref('music');
		const SearchMovies = async () => {
			await fetch(
				`https://api.themoviedb.org/3/search/movie?api_key=bac86c38508d81c3aa391db7e3be94b1&page=1&query=${search.value}`,
			)
				.then(response => response.json())
				.then(result => {
					console.log(result);
					movies.value = result.results;
					search.value = '';
				})
				.catch(error => console.log(error));
		};
		SearchMovies();
		const TopMovies = async () => {
			await fetch(
				`https://api.themoviedb.org/3/movie/popular?api_key=bac86c38508d81c3aa391db7e3be94b1`,
			)
				.then(response => response.json())
				.then(result => (sliders.value = result.results))
				.catch(error => console.log(error));
		};
		TopMovies();
		return {
			movies,
			sliders,
			search,
			SearchMovies,
			TopMovies,
			modules: [EffectCoverflow, Pagination, Autoplay],
		};
	},
};
</script>

<style lang="scss">
.movie__inner {
	ul {
		display: flex;
		justify-content: space-between;
		flex-wrap: wrap;
		li {
			width: 23%;
			position: relative;
			em {
				display: block;
				height: 80px;
				margin-bottom: 30px;
				font-family: var(--font-kor2);
			}
			.title {
				padding: 5px 0;
				display: inline-block;
			}
			.star {
				background: rgba(255, 255, 255, 0.5);
				color: #000;
				position: absolute;
				left: 20px;
				top: 20px;
				width: 30px;
				height: 30px;
				border-radius: 50px;
				text-align: center;
				line-height: 30px;
				font-weight: 800;
			}
		}
	}
	a {
		color: var(--white);
	}
}

.movie__search {
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
		background: #fff;
		border: 1px solid #000;
		border-radius: 50px;
		width: 100%;
		padding: 14px 20px;
		font-family: var(--font-kor);
	}
	button {
		position: absolute;
		right: 15px;
		top: 8px;
		width: 40px;
		height: 40px;
		border: 0;
		font-family: var(--font-kor);
		font-weight: 400;
		cursor: pointer;
		z-index: 1000;
		background: #fff;
	}
}

.movie__list {
	display: flex;
	justify-content: space-between;
	margin: 0 auto;
	margin-bottom: 100px;
	align-items: flex-end;

	h2 {
		color: var(--white);
		font-size: 2vw;
		font-family: var(--font-main);
	}

	p {
		color: var(--white);
		font-size: 1vw;
		font-family: var(--font-kor);
		font-weight: 400;
	}
	img {
		margin-bottom: 30px;
	}
}

#app {
	height: 100%;
}
html,
.movie__slider {
	position: relative;
	height: 100%;
}

.movie__slider {
	background: #fff;
	font-family: Helvetica Neue, Helvetica, Arial, sans-serif;
	font-size: 14px;
	color: #000;
	margin: 0;
	padding: 0;
}

.swiper {
	width: 100%;
	padding-top: 50px;
	padding-bottom: 230px;
}

.swiper-slide {
	background-position: center;
	background-size: cover;
	width: 300px;
	height: 300px;
}

.swiper-slide img {
	display: block;
	width: 100%;
}

.score {
	font-weight: 800;
	border-bottom: 1px solid #000;
	color: #000;
	right: 0px;
	width: 30px;
	top: -30px;
	position: absolute;
	height: 23px;
	text-align: center;
}
.title {
	padding: 5px 0;
	display: inline-block;
	color: #000;
	font-size: 16px;
	font-family: var(--font-kor);
}
</style>
