<script>
	import { onMount } from 'svelte';
	import { language } from '$lib/stores/language';
	import { translations } from '$lib/i18n/translations';
	import CountUp from 'svelte-countup';
	import PlatformFeatures from '$lib/components/PlatformFeatures.svelte';
	import ResultsComparison from '$lib/components/ResultsComparison.svelte';
	import ECGShowcase from '$lib/components/ECGShowcase.svelte';
	import ContactForm from '$lib/components/ContactForm.svelte';

	$: t = translations[$language];
</script>

<svelte:head>
	<title>DeepECG.ai - AI-Powered ECG Analysis Platform</title>
	<meta name="description" content="Advanced AI-powered ECG analysis for healthcare professionals" />
</svelte:head>

<main class="pt-16">
	<!-- Hero Section -->
	<section class="gradient-bg text-white py-20 md:py-32">
		<div class="container mx-auto px-4">
			<div class="max-w-5xl mx-auto text-center">
				<h1 class="text-4xl md:text-6xl font-bold mb-6">
					{t.title}
				</h1>
				<p class="text-xl mb-8 text-gray-100">
					{t.subtitle}
				</p>
				<div class="flex items-center justify-center gap-4">
					<a
						href="#contact"
						class="inline-block bg-white text-primary px-8 py-4 rounded-lg font-bold hover:bg-gray-100 transition-all duration-200 transform hover:scale-105 shadow-lg"
					>
						{t.getStarted}
					</a>
					<a
						href="/login"
						class="inline-block bg-[#002F63] text-white px-8 py-4 rounded-lg font-bold hover:bg-[#00254F] transition-all duration-200 transform hover:scale-105 shadow-lg border border-white/20"
					>
						{t.login}
					</a>
				</div>
			</div>
		</div>
	</section>

	<PlatformFeatures />

	<ECGShowcase />

	<!-- How It Works -->
	<section id="features" class="py-20 bg-gray-50">
		<div class="container mx-auto px-4">
			<h2 class="text-3xl md:text-4xl font-bold text-center mb-16">{t.howItWorks}</h2>
			<div class="grid md:grid-cols-3 gap-8">
				{#each [
					{
						title: t.steps.connect.title,
						description: t.steps.connect.description,
						icon: '🔌'
					},
					{
						title: t.steps.upload.title,
						description: t.steps.upload.description,
						icon: '☁️'
					},
					{
						title: t.steps.results.title,
						description: t.steps.results.description,
						icon: '📋'
					}
				] as step}
					<div class="bg-white p-6 rounded-lg shadow-lg text-center">
						<div class="text-4xl mb-4">{step.icon}</div>
						<h3 class="text-xl font-bold mb-2">{step.title}</h3>
						<p class="text-gray-600">{step.description}</p>
					</div>
				{/each}
			</div>
		</div>
	</section>

	<!-- Performance Metrics -->
	<section id="performance" class="py-20">
		<div class="container mx-auto px-4">
			<h2 class="text-3xl md:text-4xl font-bold text-center mb-8">{t.performanceMetrics}</h2>
			<div class="grid md:grid-cols-3 gap-8">
				{#each [
					{ metric: 99, label: t.accuracyRate },
					{ metric: 1, label: t.processingTime, noPercent: true },
					{ metric: 2000000, label: t.ecgsAnalyzed, noPercent: true }
				] as stat}
					<div class="text-center">
						<div class="text-4xl font-bold text-[#00509E] mb-2">
							<CountUp
								initial={0}
								value={stat.metric}
								duration={2000}
								decimals={stat.metric === 99 ? 1 : 0}
								options={{ separator: ',' }}
							/>
							{stat.noPercent ? '' : '%'}
						</div>
						<p class="text-gray-600">{stat.label}</p>
					</div>
				{/each}
			</div>
			<div class="mt-16">
				<ResultsComparison />
			</div>
		</div>
	</section>

	<!-- Validation -->
	<section id="validation" class="py-20 bg-gray-50">
		<div class="container mx-auto px-4">
			<h2 class="text-3xl md:text-4xl font-bold text-center mb-16">{t.clinicalValidation}</h2>
			<div class="grid md:grid-cols-2 gap-12">
				<div class="bg-white p-8 rounded-lg shadow-lg">
					<h3 class="text-2xl font-bold mb-4">{t.detectionRates}</h3>
					<ul class="space-y-4">
						<li class="flex items-center">
							<span class="w-3 h-3 bg-primary rounded-full mr-3" />
							<span>{t.detection.afib}</span>
						</li>
						<li class="flex items-center">
							<span class="w-3 h-3 bg-primary rounded-full mr-3" />
							<span>{t.detection.lvh}</span>
						</li>
						<li class="flex items-center">
							<span class="w-3 h-3 bg-primary rounded-full mr-3" />
							<span>{t.detection.st}</span>
						</li>
					</ul>
				</div>
				<div class="bg-white p-8 rounded-lg shadow-lg">
					<h3 class="text-2xl font-bold mb-4">{t.clinicalApplications}</h3>
					<ul class="space-y-4">
						<li class="flex items-center">
							<span class="w-3 h-3 bg-accent rounded-full mr-3" />
							<span>{t.applications.early}</span>
						</li>
						<li class="flex items-center">
							<span class="w-3 h-3 bg-accent rounded-full mr-3" />
							<span>{t.applications.remote}</span>
						</li>
						<li class="flex items-center">
							<span class="w-3 h-3 bg-accent rounded-full mr-3" />
							<span>{t.applications.emergency}</span>
						</li>
					</ul>
				</div>
			</div>
		</div>
	</section>

	<!-- Contact -->
	<section id="contact" class="py-20">
		<div class="container mx-auto px-4">
			<h2 class="text-3xl md:text-4xl font-bold text-center mb-4">
				{$language === 'en' ? 'Contact Us' : 'Contactez-nous'}
			</h2>
			<p class="text-center text-gray-600 mb-12 max-w-2xl mx-auto">
				{t.contactMessage}
			</p>
			<ContactForm />
		</div>
	</section>
</main>