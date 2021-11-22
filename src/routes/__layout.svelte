<script>
	import '../app.css';
	import anime from 'animejs/lib/anime.es';

	let listHoverIn = (list) => {
		anime({
			targets: list.srcElement,
			translateX: 20,
			easing: 'linear',
			duration: 100,
		});
		// Moving chevron
		chevronMoving().play();
	}
	let listHoverOut = (list) => {
		anime({
			targets: list.srcElement,
			translateX: 0,
			easing: 'linear',
			duration: 100
		})
	}
	let chevronMoving = () => {
		return anime({
			targets: list.srcElement.querySelector('svg'),
			translateX: -10,
			loop: true,
			duration: 300,
			easing: 'linear',
			direction: 'alternate', 
		});
	}
</script>

<slot />

<footer class="bg-gray-900 text-gray-200 pb-32">
	<p class="attribution p-6 text-center text-sm">
		Challenge by <a class="transition hover:text-custom-red" href="https://www.frontendmentor.io?ref=challenge" target="_blank">Frontend Mentor</a>. 
		Coded by <a class="transition hover:text-custom-red" href="https://github.com/joelepore" target="_blank">Giuseppe Lepore</a>.
	</p>
	<section class="max-w-2xl mx-auto text-3xl font-bold">
		<h4 class="text-custom-red">
			This project was built with:
		</h4>
		<div class="w-full grid py-5 gap-10 md:grid-cols-3">
			<ul class="col-span-2">
				<li on:mouseenter={listHoverIn} on:mouseleave={listHoverOut} class="relative cursor-pointer transition hover:text-custom-red">
					<a href="https://kit.svelte.dev" target="_blank">
						<svg class="w-[1em] h-[1em] top-0.5 absolute left-[-1em] block" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path></svg>
						SvelteKit
						<p class="text-sm font-light">JavaScript Frontend Framework</p>
					</a>
				</li>
				<li on:mouseenter={listHoverIn} on:mouseleave={listHoverOut} class="relative cursor-pointer transition hover:text-custom-red">
					<a href="https://tailwindcss.com" target="_blank">
						<svg class="w-[1em] h-[1em] top-0.5 absolute left-[-1em] block" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path></svg>
						TailwindCSS	
						<p class="text-sm font-light">CSS Frontend Framework</p>
					</a>
				</li>
				<li on:mouseenter={listHoverIn} on:mouseleave={listHoverOut} class="relative cursor-pointer transition hover:text-custom-red">
					<a href="https://animejs.com" target="_blank">
						<svg class="w-[1em] h-[1em] top-0.5 absolute left-[-1em] block" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path></svg>
						Anime.js	
						<p class="text-sm font-light">Animations Library</p>
					</a>
				</li>
			</ul>

			<div id="right-content" class="text-base text-custom-red font-normal col-span-1">
				<ul class="space-y-3">
					<li>
						<a href="#">Check the GitHub repository</a>
					</li>
					<li>
						<a href="#">Check the original FrontendMentor project page</a>
					</li>
					<li>
						<a href="#">SvelteKit + TailwindCSS template I use</a>
					</li>
				</ul>
			</div>
			
		</div>
	</section>
</footer>

<style>
	#right-content > ul li:hover {
		text-decoration: underline;
	}
	#right-content > ul li{
		transition: .1s;
	}
</style>