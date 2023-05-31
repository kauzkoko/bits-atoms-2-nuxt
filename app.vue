<template>
	<div class="card" @click="transition" :style="styleRotateY">
		<!-- Write your markup in here! Feel free to delete the title and the text! -->
		<h1 class="title" :style="styleSkew">Piazzale Delfino</h1>
		<div class="content-wrapper" :style="styleRotate">
			<div class="content">
				<img class="image" src="/scaledpiazzale.jpg" alt="An outlook to the Delfino Square" />
				<div class="prop h">
					<div>Difficulty</div>
					<div>High</div>
				</div>
				<div class="prop h">
					<div>Rounds</div>
					<div>3</div>
				</div>
				<div class="prop v">
					<div>Boosts</div>
					<div>Ramps, boost pads</div>
				</div>
				<div class="prop v">
					<div>Obstacles</div>
					<div>Palm trees, flower beds</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script setup>
useHead({
	link: [
		{
			rel: "preconnect",
			href: "https://cdn.fonts.net",
		},
		{
			rel: "stylesheet",
			href: "https://cdn.fonts.net/kit/f87cf0be-2572-4751-92fa-f4e8273843fb/f87cf0be-2572-4751-92fa-f4e8273843fb.css",
		},
	],
})

const { width, height } = useWindowSize()
const { x, y } = useMouse()
const source = ref(0)
const transition = () => {
	source.value = source.value === 0 ? 360 : 0
}

const output = useTransition(source, {
  duration: 1000,
})

const styleSkew = computed(() => {
	return {
		transform: `skew(${output.value/2}deg, ${output.value/2}deg)`,
	}
})

const styleRotate = computed(() => {
	return {
	transform: `rotate3d(1, 1, 1, ${output.value}deg)`,
	}
})

const styleRotateY = computed(() => {
	return {
		transform: `rotate3d(0, 1, 0, ${output.value}deg) translate(${x.value/100}px, ${y.value/100}px)`,
	}
})
</script>

<style>
/** 
 * A very basic CSS reset:
 * More about CSS resets: https://meyerweb.com/eric/tools/css/reset/
 */
* {
	box-sizing: border-box;
	margin: 0;
	padding: 0;
	font-size: 12px;
}

/** 
 * Card sizing and positioning.
 * Don't mess with this!
 */
.card {
	width: 300px;
	height: 540px;
	margin: 40px auto 0 auto;
	font-family: "ClobberinTimeSmooth";
	padding: 40px 40px;
	background: radial-gradient(50% 50% at 50% 50%, #ffffff 0%, #6b9fe4 100%);
	border-radius: 8px;
	transition: all .1s;
}

/** 
 * Just some styling to make the card visible.
 * Feel free to change this!
 */

.title {
	margin: 0;
	text-align: center;
	font-size: 4em;
	stroke: #172951 3px;
	text-transform: uppercase;
	background: linear-gradient(180deg, #bb9a1a 0%, #f6dd80 100%);
	-webkit-background-clip: text;
	-webkit-text-fill-color: transparent;
	-webkit-text-stroke: 2px #000;
}

.content-wrapper {
	margin: 10px 0;
	background: linear-gradient(180deg, #2927f4 50%, rgba(41, 39, 244, 0) 100%);
	border: 1px solid #000000;
	box-shadow: 2px 2px 2px #000000, inset 2px 2px 2px #ffffff;
	border-radius: 5px;
}

.content {
	padding: 20px;
	position: relative;
}

.image {
	width: 100%;
	border: solid black 1px;
	border-radius: 5px;
}

.prop {
	margin: 8px 0;
	-webkit-text-stroke: 0.5px #000;
}

.prop.h {
	display: flex;
	justify-content: space-between;
	align-items: center;
}

.prop div:first-child {
	color: white;
	font-size: 1.5em;
}

.prop div:last-child {
	color: #f9c300;
	font-size: 1em;
}
</style>
