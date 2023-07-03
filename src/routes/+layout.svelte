<script lang='ts'>
	// The ordering of these imports is critical to your app working properly
	import '@skeletonlabs/skeleton/themes/theme-skeleton.css';
	// If you have source.organizeImports set to true in VSCode, then it will auto change this ordering
	import '@skeletonlabs/skeleton/styles/skeleton.css';
	// Most of your app wide CSS should be put in this file
	import '../app.postcss';
	import { AppShell } from '@skeletonlabs/skeleton';
	import { AppBar } from '@skeletonlabs/skeleton';
	import { Avatar } from '@skeletonlabs/skeleton';
	import { Drawer, drawerStore } from '@skeletonlabs/skeleton';
	import type { DrawerSettings } from '@skeletonlabs/skeleton';
	//Drawer Function Open Here
	function trigger(position: 'left' | 'top' | 'right' | 'bottom'): void {
		const s: DrawerSettings = { id: 'demo', position };
		drawerStore.open(s);
	}
	function triggerStyled(): void {
		const drawerSettings: DrawerSettings = {
			id: 'demo',
			// Property Overrides
			position: 'left',
			bgDrawer: 'bg-purple-900 text-white',
			bgBackdrop: 'bg-gradient-to-tr from-indigo-500/50 via-purple-500/50 to-pink-500/50',
			width: 'w-[280px] md:w-[800px]',
			padding: 'p-4',
			rounded: 'rounded-xl',
			// Metadata
			meta: 'Styled Drawer'
		};
		drawerStore.open(drawerSettings);
	}
	//Drawer Function Close Here
	
	// Add A new card 
	function addNewCard() {
    let cardName = prompt("Enter the name of the card:");
    const imageURL = prompt("Enter the URL for the image:");
    let cardContainer = document.querySelector('.w-full');
    if (cardName && imageURL) {

      let newCard = document.createElement('a');

      const img = document.createElement('img');
      img.src = imageURL;
      img.alt = cardName + " Logo";
      img.className = "card-image";

      const cardTitle = document.createElement('div');
      cardTitle.textContent = cardName;
      cardTitle.className = "text-center mt-2";

      newCard.appendChild(img);
      newCard.appendChild(cardTitle);

      newCard.href = "#";
      newCard.className = "block card card-hover p-4 square-card white-card"; // Apply the necessary classes

      cardContainer?.appendChild(newCard);
    }
  }

	// Add a new card code end here
</script>
<Drawer>
	<h1 class="text-3xl px-10 py-5 text-center">Explore Cars</h1>
	<div>
		<button class="col-span-2 btn variant-filled" on:click={addNewCard}>+ Add </button>
	  </div>
	<div class="w-full text-token grid grid-cols-1 md:grid-cols-2 gap-4">
	  <a href="/cars/toyota" class="block card card-hover p-4 square-card white-card">
		<img src="https://www.logotaglines.com/wp-content/uploads/2017/01/toyota-logo-344x365.jpg" alt="Toyota Logo" class="card-image" />
		<div class="text-center mt-2">Toyota</div>
	  </a>
	  <a href="/cars/suzuki" class="block card card-hover p-4 square-card white-card">
		<img src="https://e7.pngegg.com/pngimages/240/984/png-clipart-suzuki-logo-suzuki-carry-suzuki-carry-suzuki-jimny-honda-logo-suzuki-angle-emblem-thumbnail.png" alt="Suzuki Logo" class="card-image" />
		<div class="text-center mt-2">Suzuki</div>
	  </a>
	  
	</div>
  </Drawer>
  
  
  <style>
	.square-card {
	  width: 200px; /* Adjust the width as needed */
	  height: 200px; /* Equal to the width to maintain a square shape */
	  border-radius: 8px; /* Optional: Add rounded corners */
	  margin-bottom: 20px;
	  margin-left: 90px;
	}
  
	.white-card {
	  background-color: white;
	}
  
	@media (min-width: 768px) {
	  .grid-cols-1 {
		grid-template-columns: repeat(2, minmax(0, 1fr));
	  }
	}
  </style>
  
  
  
<AppShell>
	<svelte:fragment slot="header">
		<AppBar gridColumns="grid-cols-3" class = "p-2" slotDefault="place-self-center" slotTrail="place-content-end">
			<svelte:fragment slot="lead">
				<button class="col-span-2 btn variant-filled" on:click={triggerStyled}>Explore</button>
				
			</svelte:fragment>
			<h1 class="text-3xl px-10 py-5 text-center">CARS</h1>

			<svelte:fragment slot="trail"><Avatar initials="HA" background="bg-primary-500" border="border-4 border-surface-300-600-token hover:!border-primary-500"
			cursor="cursor-pointer"/></svelte:fragment>
		</AppBar>
	</svelte:fragment>

	<!--<svelte:fragment slot="pageHeader">Page Header</svelte:fragment>-->
	<!-- Router Slot -->
	<slot />
	<!-- ---- / ---- -->
	<svelte:fragment slot="pageFooter"></svelte:fragment>
	<svelte:fragment slot="footer"></svelte:fragment>
</AppShell>
<slot />
