<script lang="ts">
  import { onMount } from 'svelte';
  import { page } from '$app/stores';
	import { trackEvent } from '@aptabase/web';
	import { goto } from '$app/navigation';
  import { onSearchPage } from '$lib/stores';

  function openSettingsMenu() {
    trackEvent("click:openSettingsMenu");
    goto('/settings');
    // window.menuAPI?.showSettingsMenu();
  }

  let onSettingsSubPage = false;

  onMount(() => {
		// add an event listener to every time the page changes
		page.subscribe((value) => {
			const route = value.url.pathname;
			if (route) {
				if (route === '/search') {
          $onSearchPage = true;
        } else {
          $onSearchPage = false;
          if (route.startsWith('/settings/')) {
            onSettingsSubPage = true;
          } else {
            onSettingsSubPage = false;
          }
        }
			}
		});
	});

</script>

<div id="settings-button-div" class="no-drag">
  {#if $onSearchPage}
    <button class="btn link-dark" title="Open Settings" on:click={() => openSettingsMenu()}>
      <i id="settings-button" class="bi bi-gear" aria-label="Settings" aria-hidden="true"/>
    </button>
  {:else}
    {#if onSettingsSubPage}
      <a href="/settings" id="settings-button" class="d-block link-dark" title="Back to Settings">
        <i class="bi bi-arrow-left-short" aria-label="Back"></i>
        <i class="bi bi-gear" aria-label="Settings"/>
      </a>
    {:else}
      <a href="/search" id="search-button" class="d-block link-dark" title="Back to Search">
        <i class="bi bi-arrow-left-short" aria-label="Back"></i>
        <i class="bi bi-search" aria-label="Search"/>
      </a>
    {/if}
  {/if}
</div>

<style>
  .btn:active {
    border-color: transparent;
  }
  .btn:hover,
  .btn:focus {
    border-color: transparent;
    transform: rotate(60deg);
    color: var(--hot-pink) !important;
  }

  a:hover {
    transform: scale(1.1);
    color: var(--hot-pink) !important;
  }

  a {
    text-decoration: none !important;
  }
</style>