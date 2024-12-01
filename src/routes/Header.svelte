<script>
	import { page } from '$app/stores';
	import LanguageToggle from '$lib/components/LanguageToggle.svelte';
	import logo from '$lib/images/logo.svg';
</script>

<header class="fixed w-full top-0 z-50 bg-white/90 backdrop-blur-sm shadow-sm">
	<div class="container mx-auto px-4">
		<div class="flex items-center justify-between h-16">
			<div class="flex items-center">
				<a href="/" class="flex items-center gap-3 text-2xl font-bold text-primary">
					<img src={logo} alt="DeepECG Logo" class="w-8 h-8" />
					DeepECG<span class="text-secondary">.ai</span>
				</a>
			</div>

			<nav class="hidden md:flex space-x-8">
				<a
					href="#features"
					class="text-black/70 hover:text-primary transition-colors duration-200">
					Features</a
				>
				<a
					href="#performance"
					class="text-black/70 hover:text-primary transition-colors duration-200">
					Performance</a
				>
				<a
					href="#validation"
					class="text-black/70 hover:text-primary transition-colors duration-200">
					Validation</a
				>
				<a href="#contact" class="btn-primary">Contact Us</a>
				<LanguageToggle />
			</nav>

			<button class="md:hidden p-2" aria-label="Menu">
				<svg
					class="w-6 h-6"
					fill="none"
					stroke="currentColor"
					viewBox="0 0 24 24"
					xmlns="http://www.w3.org/2000/svg"
				>
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						stroke-width="2"
						d="M4 6h16M4 12h16M4 18h16"
					/>
				</svg>
			</button>
		</div>
	</div>
</header>