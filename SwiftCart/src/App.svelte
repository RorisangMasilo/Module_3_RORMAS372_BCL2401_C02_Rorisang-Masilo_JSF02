<script>
  // @ts-ignore
  import { Router, Route } from 'svelte-routing';
  import Header from './components/Header.svelte';
  import ProductList from './components/ProductList.svelte';
  import ProductDetail from './components/ProductDetail.svelte';
  import { onMount } from 'svelte';

  let products = [];

  const fetchProducts = async () => {
    const res = await fetch('https://fakestoreapi.com/products');
    products = await res.json();
  };

  onMount(() => {
    fetchProducts();
  });
</script>

<Router>
  <Header />
  <div class="container">
    <Route path="/" let:params>
      <ProductList {products} />
    </Route>
    <Route path="/product/:id" let:params>
      <ProductDetail {params} />
    </Route>
  </div>
</Router>
