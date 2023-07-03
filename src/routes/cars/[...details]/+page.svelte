<script lang="ts">
    import { page } from "$app/stores";
  
    let detailArr:string[] = [];
    
  
    // Subscribe to the page store and update detailArr when the route changes
    $: {
      const params = $page.params;
      detailArr = params.details ? params.details.split('/') : [];
    }
  
    function addNewCard() {
    const cardName = prompt("Enter the name of the card:");
    const imageURL = prompt("Enter the URL for the image:");
    const cardContainer = document.querySelector('.card-grid');

    if (cardName && imageURL && cardContainer) {
      const newCard = document.createElement('div');
      newCard.className = "card";

      const img = document.createElement('img');
      img.src = imageURL;
      img.alt = cardName + " Logo";

      const cardTitle = document.createElement('div');
      cardTitle.textContent = cardName;
      cardTitle.className = "text-center mt-2";

      newCard.appendChild(img);
      newCard.appendChild(cardTitle);

      // Insert the new card after the 3rd card
      const thirdCard = cardContainer.children[2];
      cardContainer.insertBefore(newCard, thirdCard.nextSibling);
    }
  }
  </script>
  <div class="card-container">
    <div class="button-container">
      <button class="col-span-2 btn variant-filled" on:click={addNewCard}>Add New Car</button>
    </div>
    {#if detailArr[0] === "toyota"}
      <h1 class="text-3xl px-10 py-5 text-center add-car-button">Toyota Cars</h1>
      <div class="card-grid">
        {#each Array(2) as _, i}
          <div class="card">
            <!-- Card content here -->
            {#if i === 0}
              <img src="https://imgd.aeplcdn.com/664x374/n/cw/ec/140809/innova-crysta-exterior-right-front-three-quarter.png?isig=0&q=75" alt="Toyota Card 1" class="card-image"/>
            {:else if i === 1}
              <img src="https://imgd.aeplcdn.com/0x0/n/cw/ec/44709/fortuner-exterior-right-front-three-quarter-19.jpeg" alt="Toyota Card 2" class="card-image"/>
            {:else}
              Card {i+1}
            {/if}
          </div>
        {/each}
      </div>
    {:else if detailArr[0] === "suzuki"}
      <h1 class="text-3xl px-10 py-5 text-center">Suzuki Cars</h1>
      <div class="card-grid">
        {#each Array(2) as _, i}
          <div class="card">
            <!-- Different card content for Suzuki -->
            {#if i === 0}
              <img src="https://imgd.aeplcdn.com/664x374/n/cw/ec/107543/vitara-brezza-2022-exterior-right-front-three-quarter.jpeg?isig=0&q=75" alt="Suzuki Card 1" class="card-image"/>
            {:else if i === 1}
              <img src="https://images.91wheels.com//assets/c_images/gallery/maruti/dzire/maruti-dzire-15-1598096804.jpg?width=420&q=60?w=1080&q=60" alt="Suzuki Card 2" class="card-image"/>
            {:else}
              Card {i+1}
            {/if}
          </div>
        {/each}
      </div>
    {:else}
      <h1>Other Cards</h1>
      <!-- Render cards for other options -->
    {/if}
  </div>
  
  <style>
    .card-container {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
    }
  
    .card-grid {
      display: grid;
      grid-template-columns: repeat(5, 1fr); /* Update to 5 columns */
      grid-gap: 10px;
    }
  
    .card {
      width: 200px;
      height: 200px;
      background-color: white;
      border: 1px solid #ccc;
      border-radius: 4px;
      padding: 10px;
      margin-bottom: 10px;
    }
    .card-image {
      width: 100%;
      height: 100%;
      object-fit: cover;
      border-radius: 4px;
    }
  
    .button-container {
      display: flex;
      justify-content: flex-end; /* Align the button to the right */
      width: 100%;
      padding-right: 20px; /* Add some right padding for spacing */
      margin-bottom: 10px; /* Add bottom margin for spacing */
    }
  </style>