<script>
  import { language } from '$lib/stores/language';
  import { Bar, Radar } from 'svelte-chartjs';
  import {
    Chart as ChartJS,
    Title,
    Tooltip,
    Legend,
    BarElement,
    BarController,
    LinearScale,
    PointElement,
    CategoryScale,
    RadialLinearScale,
    RadarController,
    LineElement
  } from 'chart.js';

  ChartJS.register(
    Title,
    Tooltip,
    Legend,
    BarElement,
    BarController,
    LinearScale,
    PointElement,
    CategoryScale,
    RadialLinearScale,
    RadarController,
    LineElement
  );

  let activeTab = 'bar';

  const categories = ['RHYTHM', 'CONDUCTION', 'CHAMBER ENLARGEMENT', 'PERICARDITIS', 'INFARCT, ISCHEMIA', 'OTHER', 'TOTAL'];
  const healthcareSystems = {
    'Internal Dataset': {
      RHYTHM: 99.66,
      CONDUCTION: 98.99,
      'CHAMBER ENLARGEMENT': 99.02,
      PERICARDITIS: 98.77,
      'INFARCT, ISCHEMIA': 98.46,
      OTHER: 98.54,
      TOTAL: 93.18,
    },
    'Healthcare System #1': {
      RHYTHM: 98.64,
      CONDUCTION: 98.02,
      'CHAMBER ENLARGEMENT': 97.46,
      PERICARDITIS: 97.77,
      'INFARCT, ISCHEMIA': 97.26,
      OTHER: 98.68,
      TOTAL: 98.64,
    },
    'Healthcare System #2': {
      RHYTHM: 99.10,
      CONDUCTION: 97.64,
      'CHAMBER ENLARGEMENT': 97.58,
      PERICARDITIS: 96.95,
      'INFARCT, ISCHEMIA': 95.89,
      OTHER: 98.88,
      TOTAL: 98.60,
    },
    'Healthcare System #3': {
      RHYTHM: 99.25,
      CONDUCTION: 95.23,
      'CHAMBER ENLARGEMENT': 87.78,
      PERICARDITIS: 92.63,
      'INFARCT, ISCHEMIA': 81.19,
      OTHER: 96.04,
      TOTAL: 97.82,
    },
  };

  const chartColors = {
    'Internal Dataset': '#548FDF',
    'Healthcare System #1': '#82C0F2',
    'Healthcare System #2': '#8EE4AA',
    'Healthcare System #3': '#181E27'
  };

  const barChartData = {
    labels: categories,
    datasets: Object.entries(healthcareSystems).map(([system, data]) => ({
      label: system,
      data: categories.map(category => data[category]),
      borderColor: chartColors[system],
      backgroundColor: `${chartColors[system]}CC`,
      borderWidth: 1
    }))
  };

  const radarChartData = {
    labels: categories,
    datasets: Object.entries(healthcareSystems).map(([system, data]) => ({
      label: system,
      data: categories.map(category => data[category]),
      borderColor: chartColors[system],
      backgroundColor: `${chartColors[system]}33`,
      borderWidth: 2
    }))
  };

  const chartOptions = {
    responsive: true,
    maintainAspectRatio: false,
    scales: {
      x: {
        ticks: {
          maxRotation: 45,
          minRotation: 45
        }
      },
      y: {
        beginAtZero: true,
        max: 100,
        title: {
          display: true,
          text: 'Accuracy (%)',
          color: 'var(--black)'
        }
      }
    },
    plugins: {
      legend: {
        position: 'bottom',
        labels: {
          padding: 20,
          color: 'var(--black)'
        }
      }
    }
  };

  const radarOptions = {
    responsive: true,
    maintainAspectRatio: false,
    scales: {
      r: {
        beginAtZero: true,
        min: 0,
        max: 100,
        ticks: {
          stepSize: 5,
          color: '#000000'
        },
        pointLabels: {
          font: {
            size: 12,
            color: '#000000'
          }
        },
        grid: {
          color: 'rgba(0, 0, 0, 0.1)'
        },
        angleLines: {
          color: 'rgba(0, 0, 0, 0.2)'
        }
      }
    },
    plugins: {
      legend: {
        position: 'bottom',
        labels: {
          padding: 20,
          color: '#000000'
        }
      }
    }
  };
</script>

<div class="w-full max-w-4xl mx-auto bg-white rounded-lg shadow-lg p-6">
  <div class="mb-6">
    <h2 class="text-2xl font-bold text-gray-dark">
      {$language === 'en' ? 'DeepECG-SL Performance Comparison' : 'Comparaison des Performances DeepECG-SL'}
    </h2>
    <p class="text-gray-600">
      {$language === 'en' 
        ? 'Comparing DeepECG-SL performance across different healthcare systems'
        : 'Comparaison des performances DeepECG-SL à travers différents systèmes de santé'}
    </p>
  </div>

  <div class="mb-8">
    <div class="grid grid-cols-2 gap-2 p-1 bg-gray-100 rounded-lg w-64 mx-auto">
      <button
        class="px-4 py-2 rounded-md text-sm font-medium transition-colors duration-200 {activeTab === 'bar' ? 'bg-white shadow-sm text-primary' : 'hover:bg-gray-200'}"
        on:click={() => activeTab = 'bar'}
      >
        {$language === 'en' ? 'Bar Chart' : 'Graphique à Barres'}
      </button>
      <button
        class="px-4 py-2 rounded-md text-sm font-medium transition-colors duration-200 {activeTab === 'spider' ? 'bg-white shadow-sm text-primary' : 'hover:bg-gray-200'}"
        on:click={() => activeTab = 'spider'}
      >
        {$language === 'en' ? 'Spider Plot' : 'Graphique Radar'}
      </button>
    </div>
  </div>

  <div class="space-y-6">
    {#if activeTab === 'bar'}
      <div class="h-[600px]">
        <Bar data={barChartData} options={chartOptions} />
      </div>
    {:else}
      <div class="h-[600px]">
        <Radar data={radarChartData} options={radarOptions} />
      </div>
    {/if}
  </div>
</div>