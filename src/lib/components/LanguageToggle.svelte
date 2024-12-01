<script>
  import { language } from '$lib/stores/language';

  function toggleLanguage() {
    $language = $language === 'en' ? 'fr' : 'en';
  }
</script>

<button
  on:click={toggleLanguage}
  class="px-3 py-1 rounded-md bg-white/10 hover:bg-white/20 transition-colors duration-200 text-sm font-medium"
>
  {$language === 'en' ? 'FR' : 'EN'}
</button>