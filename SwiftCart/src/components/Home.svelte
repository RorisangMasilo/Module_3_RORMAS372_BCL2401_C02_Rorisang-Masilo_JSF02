<!-- <script>
  export let products = [];
  export let loading = true;
  export let selectedCategory = "";
  export let sortOrder = "";
  export let filteredProductsList = [];
  export let categories = [];
  export let goToProductDetails;

  function filterProducts() {
    let tempProducts = products;

    if (selectedCategory) {
      tempProducts = tempProducts.filter(
        (product) => product.category === selectedCategory
      );
    }

    if (sortOrder === "asc") {
      tempProducts = tempProducts.sort((a, b) => a.price - b.price);
    } else if (sortOrder === "desc") {
      tempProducts = tempProducts.sort((a, b) => b.price - a.price);
    }

    filteredProductsList = tempProducts;
  }

  function resetFilters() {
    selectedCategory = "";
    sortOrder = "";
    filteredProductsList = products;
  }
</script>

<div class="container mx-auto px-6 py-8">
  <div class="flex justify-between items-center mb-4">
    <div>
      <label for="category" class="text-xl font-semibold mr-2 text-primary-dark">Category:</label>
      <select bind:value={selectedCategory} on:change={filterProducts} class="border rounded p-2">
        <option value="">All</option>
        {#each categories as category}
          <option value={category}>{category}</option>
        {/each}
      </select>
    </div>

    <div>
      <label for="sort" class="text-xl font-semibold mr-2 text-primary-dark">Sort by price:</label>
      <select bind:value={sortOrder} on:change={filterProducts} class="border rounded p-2">
        <option value="">Default</option>
        <option value="asc">Lowest to Highest</option>
        <option value="desc">Highest to Lowest</option>
      </select>
    </div>
  </div>

  <div>
    <button
      on:click={resetFilters}
      class="bg-primary-dark text-primary-light font-semibold py-2 px-4 rounded"
    >
      Reset
    </button>
  </div>
</div>

{#if loading}
  <div class="loading text-center text-2xl text-primary-accent1">
    Loading...
  </div>
{:else}
  <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
    {#each filteredProductsList as product (product.id)}
      <div
        class="card bg-primary-light shadow rounded-lg border-primary-dark p-4 hover:shadow-lg transition-shadow duration-300 flex flex-col items-center"
        on:click={() => goToProductDetails(product.id)}
      >
        <div class="flex justify-center w-full mb-4">
          <img
            src={product.image}
            alt="Product Image"
            class="h-32 w-full object-contain mb-4"
          />
        </div>
        <h2 class="text-lg font-semibold mb-2 text-primary-dark">{product.title}</h2>
        <p class="text-gray-600 mb-2">${product.price}</p>
        <p class="text-gray-600 mb-2">{product.category}</p>
        <div class="flex items-center">
          {#each Array(5) as _, i}
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="currentColor"
              viewBox="0 0 22 20"
              class="w-4 h-4 ml-1"
              class:text-primary-accent2={i < Math.round(product.rating.rate)}
              class:text-primary-medium={i >= Math.round(product.rating.rate)}
            >
              <path
                d="M20.924 7.625a1.523 1.523 0 0 0-1.238-1.044l-5.051-.734-2.259-4.577a1.534 1.534 0 0 0-2.752 0L7.365 5.847l-5.051.734A1.535 1.535 0 0 0 1.463 9.2l3.656 3.563-.863 5.031a1.532 1.532 0 0 0 2.226 1.616L11 17.033l4.518 2.375a1.534 1.534 0 0 0 2.226-1.617l-.863-5.03L20.537 9.2a1.523 1.523 0 0 0 .387-1.575Z"
              />
            </svg>
          {/each}
          <span class="ml-2 text-sm text-gray-600">{product.rating.count} reviews</span>
        </div>
      </div>
    {/each}
  </div>
{/if} -->
