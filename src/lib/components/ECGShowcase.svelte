<script>
  import { onMount } from 'svelte';
  import { language } from '$lib/stores/language';
  import { translations } from '$lib/i18n/translations';
  import ecgAnalysis from '$lib/images/ecg-analysis.png';
  
  let activeFeature = null;
  let imageLoaded = false;
  let hoveredFeature = null;

  $: t = translations[$language];
  
  onMount(() => {
    const img = new Image();
    img.src = ecgAnalysis;
    img.onload = () => {
      imageLoaded = true;
    };
  });

  const features = [
    {
      id: 'patient-info',
      number: 1,
      title: 'Patient Information',
      description: 'Comprehensive patient details including MRN, demographics, and ECG timing',
      top: '2%',
      left: '2%',
      width: '25%'
    },
    {
      id: 'measurements',
      number: 2,
      title: 'ECG Measurements',
      description: 'Key measurements including ventricular rate, PR interval, QRS duration',
      top: '2%',
      left: '32%',
      width: '25%'
    },
    {
      id: 'ai-predictions',
      number: 3,
      title: 'AI Predictions',
      description: 'Advanced AI analysis with confidence scores for various ECG patterns',
      top: '35%',
      right: '2%',
      width: '25%'
    },
    {
      id: 'ecg-chart',
      number: 4,
      title: 'ECG Visualization',
      description: 'High-resolution ECG trace with precise grid measurements',
      top: '55%',
      left: '5%',
      width: '90%',
    },
  ];
</script>

<section class="py-20 bg-white relative z-10"
>
  <div class="container mx-auto px-4">
    <h2 class="text-4xl font-bold text-center mb-16">
      Interactive ECG Analysis
    </h2>

    <div class="relative max-w-6xl mx-auto bg-white p-8 rounded-xl shadow-xl">
      {#if imageLoaded}
        <img
          src={ecgAnalysis}
          alt="ECG Analysis Interface"
          class="w-full rounded-lg shadow-md mb-8 relative"
        />
        
        <!-- Numbered Markers -->
        {#each features as feature}
          <div
            class="absolute w-8 h-8 rounded-full bg-primary text-white flex items-center justify-center font-bold shadow-lg transform transition-all duration-300 cursor-pointer hover:scale-110"
            style="top: {feature.top}; {feature.left ? `left: ${feature.left}` : `right: ${feature.right}`};"
            on:mouseenter={() => (hoveredFeature = feature.id)}
            on:mouseleave={() => (hoveredFeature = null)}
          >
            {feature.number}
          </div>
        {/each}
      {:else}
        <div class="w-full h-96 bg-gray-100 rounded-lg animate-pulse mb-8" />
      {/if}

      {#each features as feature}
        <div
          class="absolute cursor-pointer transition-all duration-300 opacity-0 group"
          class:opacity-100={hoveredFeature === feature.id}
          class:z-50={hoveredFeature === feature.id}
          style="top: {feature.top}; {feature.left ? `left: ${feature.left}` : `right: ${feature.right}`}; width: {feature.width};"
          on:mouseenter={() => (hoveredFeature = feature.id)}
          on:mouseleave={() => (hoveredFeature = null)}
        >
          <div
            class="bg-white/95 backdrop-blur-sm rounded-lg p-4 shadow-lg border-2 transform transition-all duration-300 ml-10"
            class:border-primary={hoveredFeature === feature.id} 
            class:scale-105={hoveredFeature === feature.id}
            class:border-transparent={hoveredFeature !== feature.id}
            class:shadow-xl={hoveredFeature === feature.id}
          > 
            <h3 class="text-lg font-bold text-primary mb-2">{feature.title}</h3>
            <p class="text-sm text-black/70">{feature.description}</p>
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>