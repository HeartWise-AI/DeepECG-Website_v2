<script>
  import { language } from '$lib/stores/language';
  import { translations } from '$lib/i18n/translations';

  let formData = {
    firstName: '',
    lastName: '',
    position: '',
    country: '',
    email: '',
    organization: '',
    privacyAccepted: false
  };

  $: t = translations[$language];

  const positions = [
    $language === 'en' ? 'Cardiologist' : 'Cardiologue',
    $language === 'en' ? 'Specialist (non cardiologist)' : 'Spécialiste (non cardiologue)',
    $language === 'en' ? 'Family doctor' : 'Médecin généraliste',
    $language === 'en' ? 'Researcher' : 'Chercheur',
    $language === 'en' ? 'Other' : 'Autre',
    $language === 'en' ? 'Nurse practitioner' : 'Infirmier praticien',
    $language === 'en' ? 'Clinic owner' : 'Propriétaire de clinique',
    $language === 'en' ? 'Healthcare administrator' : 'Administrateur de santé'
  ];

  const countries = [
    $language === 'en' ? 'United States' : 'États-Unis',
    'Canada',
    'France',
    $language === 'en' ? 'Germany' : 'Allemagne',
    $language === 'en' ? 'United Kingdom' : 'Royaume-Uni',
    $language === 'en' ? 'Other' : 'Autre'
  ];

  function handleSubmit() {
    console.log('Form submitted:', formData);
    // Here you would typically handle form submission
  }
</script>

<div class="w-full max-w-2xl mx-auto bg-white rounded-lg shadow-lg p-8">
  <form on:submit|preventDefault={handleSubmit} class="space-y-6">
    <div class="grid md:grid-cols-2 gap-6">
      <div>
        <label for="firstName" class="block text-sm font-medium text-black/70 mb-2">
          {$language === 'en' ? 'First Name' : 'Prénom'}
        </label>
        <input
          type="text"
          id="firstName"
          bind:value={formData.firstName}
          required
          class="w-full px-4 py-2 rounded-md border border-secondary/20 focus:border-primary focus:ring-2 focus:ring-primary/20 outline-none transition-colors"
        />
      </div>
      <div>
        <label for="lastName" class="block text-sm font-medium text-black/70 mb-2">
          {$language === 'en' ? 'Last Name' : 'Nom'}
        </label>
        <input
          type="text"
          id="lastName"
          bind:value={formData.lastName}
          required
          class="w-full px-4 py-2 rounded-md border border-secondary/20 focus:border-primary focus:ring-2 focus:ring-primary/20 outline-none transition-colors"
        />
      </div>
    </div>

    <div class="grid md:grid-cols-2 gap-6">
      <div>
        <label for="position" class="block text-sm font-medium text-black/70 mb-2">
          {$language === 'en' ? 'Position' : 'Poste'}
        </label>
        <select
          id="position"
          bind:value={formData.position}
          required
          class="w-full px-4 py-2 rounded-md border border-secondary/20 focus:border-primary focus:ring-2 focus:ring-primary/20 outline-none transition-colors"
        >
          <option value="">{$language === 'en' ? 'Select position' : 'Sélectionner un poste'}</option>
          {#each positions as position}
            <option value={position}>{position}</option>
          {/each}
        </select>
      </div>
      <div>
        <label for="country" class="block text-sm font-medium text-black/70 mb-2">
          {$language === 'en' ? 'Country' : 'Pays'}
        </label>
        <select
          id="country"
          bind:value={formData.country}
          required
          class="w-full px-4 py-2 rounded-md border border-secondary/20 focus:border-primary focus:ring-2 focus:ring-primary/20 outline-none transition-colors"
        >
          <option value="">{$language === 'en' ? 'Select country' : 'Sélectionner un pays'}</option>
          {#each countries as country}
            <option value={country}>{country}</option>
          {/each}
        </select>
      </div>
    </div>

    <div>
      <label for="email" class="block text-sm font-medium text-black/70 mb-2">
        {$language === 'en' ? 'Business email' : 'Email professionnel'}
      </label>
      <input
        type="email"
        id="email"
        bind:value={formData.email}
        required
        class="w-full px-4 py-2 rounded-md border border-secondary/20 focus:border-primary focus:ring-2 focus:ring-primary/20 outline-none transition-colors"
      />
    </div>

    <div>
      <label for="organization" class="block text-sm font-medium text-black/70 mb-2">
        {$language === 'en' ? 'Organization' : 'Organisation'}
      </label>
      <input
        type="text"
        id="organization"
        bind:value={formData.organization}
        required
        class="w-full px-4 py-2 rounded-md border border-secondary/20 focus:border-primary focus:ring-2 focus:ring-primary/20 outline-none transition-colors"
      />
    </div>

    <div class="flex items-start">
      <div class="flex items-center h-5">
        <input
          id="privacy"
          type="checkbox"
          bind:checked={formData.privacyAccepted}
          required
          class="w-4 h-4 border border-secondary/20 rounded focus:ring-2 focus:ring-primary/20"
        />
      </div>
      <label for="privacy" class="ml-2 text-sm text-black/70">
        {$language === 'en' ? 'I agree to the ' : 'J\'accepte la '}
        <a href="/privacy" class="text-primary hover:underline">
          {$language === 'en' ? 'Privacy Policy' : 'Politique de confidentialité'}
        </a>
      </label>
    </div>

    <button
      type="submit"
      class="w-full bg-primary text-white py-3 px-6 rounded-lg font-medium hover:bg-primary/90 transition-colors duration-200"
    >
      {$language === 'en' ? 'Send Message' : 'Envoyer'}
    </button>
  </form>
</div>