<script>
    import ProductCard from "./ProductCard.svelte";
    import CardSkeleton from "./CardSkeleton.svelte";
    import { useProductStore } from "../../store/productStore";
    import Error from "../Error.svelte";
  
    let products = [];
    let loading = false;
    let error = null;
  
    $: ({ products, loading, error } = useProductStore(state => ({
      products: state.products,
      loading: state.loading,
      error: state.error
    })));
  
    function renderSkeleton() {
        return Array(20).fill(null).map((_, index) => {
      return <CardSkeleton key={index} />;
    });
  }
</script>

{#if loading && !error}
  <div class="grid justify-center">
    <div class="lg:max-h-[130rem] max-w-xl mx-auto grid gap-4 grid-cols-1 lg:grid-cols-4 md:grid-cols-2 items-center lg:max-w-none my-4">
      {renderSkeleton()}
    </div>
  </div>
{:else if error}
  <div class="grid justify-center">
    <Error {...error} />
  </div>
{:else}
  <div class="grid justify-center">
    <div class="lg:max-h-[130rem] max-w-x
          {#each products as product}
        <ProductCard key={product.id} {...product} />
      {/each}
    </div>
  </div>
{/if}