<script lang="ts">
  import { invoke } from "@tauri-apps/api/core";
  import { onMount } from "svelte";
  import { fade } from "svelte/transition";
  import { goto } from "$app/navigation";
	import { trackEvent } from '@aptabase/web';
  import TopBar from "../../layout/TopBar.svelte";

	async function openInBrowser(what: string) {
		if (what === "deadline") {
			trackEvent("magic:deadline");
			await invoke("open_file_or_folder", { filePath: "https://buzo.tools/deadline/" });
		} else if (what === "bmac") {
			trackEvent("magic:bmac");
			await invoke("open_file_or_folder", { filePath: "https://www.buymeacoffee.com/thatgurjot" });
		}
	}

	function gotoMagicPage(page: string) {
		trackEvent(`magic:${page}`);
		goto(`/magic/${page}`);
	}

  onMount(() => {
		trackEvent("magic:homepage");
  })

</script>

<div in:fade={{ delay: 0, duration: 500 }}>
  
  <div class="flex flex-col gap-3 justify-content-center items-center w-4/5 pr-4 pl-4 sm:w-2/3 mx-auto">
    <div class="page-icon">
      <i class="bi bi-stars"></i>
    </div>
    <h3>Fun Stuff</h3>
    <table class="table table-bordered w-90 mb-0">
			<tr>
				<td class="text-center px-2">
					<button class="btn" on:click={() => openInBrowser("deadline")}>
            <i class="bi bi-trophy" />
					</button>
				</td>
				<td class="py-2" role="button" on:click={() => openInBrowser("deadline")}>
					Deadline<i class="bi bi-box-arrow-up-right skip-icon"></i>
					<div class="flex items-center small-explanation gap-1">
						<div>A gentle progress tracker made with kindness</div>
					</div>
				</td>
			</tr>
			<tr>
				<td class="text-center px-2">
					<button class="btn" on:click={() => gotoMagicPage('deep-breathing')}>
            <i class="bi bi-yin-yang" />
					</button>
				</td>
				<td class="py-2" role="button" on:click={() => gotoMagicPage('deep-breathing')}>
					Deep Breathing
					<div class="flex items-center small-explanation gap-1">
						<div>Take a few moments to yourself</div>
					</div>
				</td>
			</tr>
			<tr>
				<td class="text-center px-2">
					<button class="btn" on:click={() => gotoMagicPage('stats')}>
            <i class="bi bi-pie-chart" />
					</button>
				</td>
				<td class="py-2" role="button" on:click={() => gotoMagicPage('stats')}>
					Document Stats
					<div class="flex items-center small-explanation gap-1">
						<div>See what your Unique Document Profile looks like</div>
					</div>
				</td>
			</tr>
			<tr>
				<td class="text-center px-2">
					<button class="btn" on:click={() => gotoMagicPage('extract-text')}>
            <i class="bi bi-body-text" />
					</button>
				</td>
				<td class="py-2" role="button" on:click={() => gotoMagicPage('extract-text')}>
					Extract Text from PDF or Image
					<div class="flex items-center small-explanation gap-1">
						<div>Extract text from any kind of PDF or image file</div>
					</div>
				</td>
			</tr>
			<tr>
				<td class="text-center px-2">
					<button class="btn" on:click={() => gotoMagicPage('scratchpad')}>
            <i class="bi bi-journal-text" />
					</button>
				</td>
				<td class="py-2" role="button" on:click={() => gotoMagicPage('scratchpad')}>
					Scratch Pad
					<div class="flex items-center small-explanation gap-1">
						<div>A place to keep copied text, notes, and thoughts</div>
					</div>
				</td>
			</tr>
			<tr>
				<td class="text-center px-2">
					<button class="btn" on:click={() => gotoMagicPage('tips')}>
            <i class="bi bi-lightbulb" />
					</button>
				</td>
				<td class="py-2" role="button" on:click={() => gotoMagicPage('tips')}>
					Tips & Shortcuts
					<div class="flex items-center small-explanation gap-1">
						<div>Read some hints to get the best out of Buzee</div>
					</div>
				</td>
			</tr>
		</table>
  </div>
	<div class="text-center my-5">
		<p class="mb-1 small-explanation fw-medium">Show Your Appreciation</p>
		<button type="button" class="bmc-button" on:click={() => openInBrowser("bmac")}>
			<img src="https://cdn.buymeacoffee.com/buttons/bmc-new-btn-logo.svg" alt="Buy me a coffee">
			<span class="ms-2 fs-6">Buy me a coffee</span>
		</button>
	</div>
</div>

<style lang="scss">
  .small-explanation {
		font-size: 0.7rem;
		font-weight: 300;
		padding: 0;
		background-color: inherit;
		color: var(--bs-gray);
	}

	tr:hover {
    cursor: default;
    color: var(--purple);
	}

	i:not(.skip-icon) {
		font-size: 1.5rem;
	}

	i.skip-icon {
		font-size: 0.8rem;
	}

	.bmc-button img{height: 2rem !important;width: 2rem !important;margin-bottom: 1px !important;box-shadow: none !important;border: none !important;vertical-align: middle !important;}.bmc-button{padding: 7px 15px 7px 10px !important;line-height: 35px !important;height:51px !important;text-decoration: none !important;display:inline-flex !important;color:#ffffff !important;background-color:#FF813F;border-radius: 5px !important;border: 1px solid transparent !important;padding: 7px 15px 7px 10px !important;font-size: 28px !important;letter-spacing:0.6px !important;box-shadow: 0px 1px 2px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 1px 2px 2px rgba(190, 190, 190, 0.5) !important;margin: 0 auto !important;-webkit-box-sizing: border-box !important;box-sizing: border-box !important;}.bmc-button:hover, .bmc-button:active, .bmc-button:focus {-webkit-box-shadow: 0px 1px 2px 2px rgba(190, 190, 190, 0.5) !important;text-decoration: none !important;box-shadow: 0px 1px 2px 2px rgba(190, 190, 190, 0.5) !important;opacity: 0.85 !important;color:#ffffff !important;}
</style>