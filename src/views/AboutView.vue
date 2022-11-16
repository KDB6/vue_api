<template>
	<div>
		<HeaderCont />
		<TitleCont name1="About" name2="Reference API" />
		<section className="cont__about container">
			<h2>KIM DABIN</h2>
			<div className="desc__main">
				<p>
					I've been continuously<br />
					Challenging and Practicing<br />
					for the Front-End.
				</p>
			</div>
			<img src="../assets/img/my.png" alt="" />
			<div className="desc__sub">
				<h2>YOUTUBE API</h2>
				<p>
					프론트앤드를 지향하기 위해 기초부터 천천히 다져왔습니다.<br />
					각종 API를 이용하여 각 데이터를 여러 구역으로 분할하여 연습을
					해왔습니다.
				</p>
				<p>
					I've been slowly sharpening it from the basics to aim for the front
					end.<br />
					Using various APIs, each data has been divided into several areas and
					practiced.
				</p>
			</div>

			<div className="desc__sub2">
				<h2>MOVIE API</h2>
				<p>
					프론트앤드를 지향하기 위해 기초부터 천천히 다져왔습니다.<br />
					각종 API를 이용하여 각 데이터를 여러 구역으로 분할하여 연습을
					해왔습니다.
				</p>
				<p>
					I've been slowly sharpening it from the basics to aim for the front
					end.<br />
					Using various APIs, each data has been divided into several areas and
					practiced.
				</p>
			</div>

			<div className="desc__sub3">
				<h2>UNSPLASH API</h2>
				<p>
					프론트앤드를 지향하기 위해 기초부터 천천히 다져왔습니다.<br />
					각종 API를 이용하여 각 데이터를 여러 구역으로 분할하여 연습을
					해왔습니다.
				</p>
				<p>
					I've been slowly sharpening it from the basics to aim for the front
					end.<br />
					Using various APIs, each data has been divided into several areas and
					practiced.
				</p>
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

export default {
	components: {
		HeaderCont,
		FooterCont,
		TitleCont,
		ContactCont,
	},
};
</script>

<style lang="scss">
.cont__about {
	color: var(--white);
	font-family: var(--font-main);
	margin-bottom: 800px;

	h2 {
		font-size: 0.8vw;
	}
}

.desc__main {
	p {
		font-size: 5vw;
	}

	img {
		width: 500px;
		height: 500px;
	}
}

.desc__sub {
	margin-top: 150px;
	position: absolute;
	left: 50%;

	h2 {
		font-size: 1vw;
		margin-bottom: 20px;
	}

	p {
		font-family: var(--font-kor2);
		font-weight: 400;
		line-height: 1.4;
		font-size: 0.8vw;

		&:last-child {
			margin-top: 5px;
		}
	}
}

.desc__sub2 {
	margin-top: 150px;
	position: absolute;
	left: 50%;
	margin-top: 325px;

	h2 {
		font-size: 1vw;
		margin-bottom: 20px;
	}

	p {
		font-family: var(--font-kor2);
		font-weight: 400;
		line-height: 1.4;
		font-size: 0.8vw;

		&:last-child {
			margin-top: 5px;
		}
	}
}

.desc__sub3 {
	margin-top: 150px;
	position: absolute;
	left: 50%;
	margin-top: 500px;

	h2 {
		font-size: 1vw;
		margin-bottom: 20px;
	}

	p {
		font-family: var(--font-kor2);
		font-weight: 400;
		line-height: 1.4;
		font-size: 0.8vw;

		&:last-child {
			margin-top: 5px;
		}
	}
}
</style>
