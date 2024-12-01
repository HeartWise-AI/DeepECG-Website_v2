<script>
  import { language } from '$lib/stores/language';
  import { translations } from '$lib/i18n/translations';
  $: t = translations[$language];
</script>

<section class="py-20 bg-white">
  <div class="container mx-auto px-4">
    <h2 class="text-4xl md:text-5xl font-bold text-center mb-16">{t.platformFeatures.title}</h2>
    <div class="grid md:grid-cols-3 gap-8">
      {#each t.platformFeatures.features as feature}
        <div class="bg-white rounded-lg p-8 shadow-lg transition-transform hover:scale-105 duration-300 border border-secondary/20">
          <div class="text-4xl mb-4">{feature.icon}</div>
          <h3 class="text-2xl font-bold mb-4 text-primary">{feature.title}</h3>
          <p class="text-black/70">{feature.description}</p>
        </div>
      {/each}
    </div>
  </div>
</section>