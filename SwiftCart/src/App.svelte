<!-- <script>
  import Layout from './components/Layout.svelte';
  import Home from './pages/Home.svelte';
  import ProductDetailView from './pages/ProductDetailView.svelte';
  import Login from './pages/Login.svelte';
  import { onMount } from 'svelte';

  let currentRoute;

  const routes = [
    { path: '/', component: Home },
    { path: '/products/:id', component: ProductDetailView },
    { path: '/login', component: Login }
  ];
  
  function navigate(path) {
    currentRoute = path;
  }

onMount(() => {
  currentRoute = window.location.pathname;
  window.onpopstate = () => {
    currentRoute = window.location.pathname;
  };
});

function renderComponent() {
  const route = routes.find(r => r.path === currentRoute);
  return route ? route.component : Home;
}
</script>

<div>
  <Layout>
    {#await renderComponent() then Component}
      <svelte:component this={Component} />
    {/await}
  </Layout>
</div>

<style>
  @import './app.css';
</style> -->

<script>
  import { onMount } from 'svelte';
  import { Router, Route, Link } from "svelte-routing";
  import Home from './lib/components/Home.svelte';
  import ProductDetails from './lib/components/ProductDetails.svelte';

  export let url = "";

  let products = [];
  let loading = true;
  let selectedCategory = "";
  let sortOrder = "";
  let filteredProductsList = [];
  let categories = [];
  let open = false;

  onMount(() => {
    fetchProducts();
  });

  function fetchProducts() {
    loading = true;
    fetch("https://fakestoreapi.com/products")
      .then((response) => response.json())
      .then((data) => {
        products = data;
        filteredProductsList = data;
        categories = [...new Set(data.map((product) => product.category))];
        loading = false;
      });
  }

  function goToProductDetails(productId) {
    window.location.href = `/product/${productId}`;
  }
</script>

<Router {url}>
  <header>
    <nav class="bg-primary-medium border-primary-dark">
      <div class="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4">
        <Link to="/">
          <button class="flex items-center space-x-3 rtl:space-x-reverse">
            <img src="./public/logo.png" class="h-8" alt="Flowbite Logo" />
            <span class="self-center text-2xl font-semibold whitespace-nowrap text-primary-light">Emercom</span>
          </button>
        </Link>
        <button
          on:click={() => open = !open}
          class="inline-flex items-center p-2 w-10 h-10 justify-center text-sm text-white rounded-lg md:hidden hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200"
          aria-controls="navbar-default"
          aria-expanded="false"
        >
          <span class="sr-only">Open main menu</span>
          <svg
            class="w-5 h-5"
            aria-hidden="true"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 17 14"
          >
            <path
              stroke="currentColor"
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M1 1h15M1 7h15M1 13h15"
            />
          </svg>
        </button>
        <div
          class="{open ? '' : 'hidden'} w-full md:block md:w-auto"
          id="navbar-default"
        >
          <ul class="flex flex-col p-4 md:p-0 mt-4 border border-gray-100 rounded-lg bg-gray-50 md:flex-row md:space-x-8 md:mt-0 md:border-0 md:bg-white">
            <li>
              <Link to="/" class="block py-2 px-3 text-primary-dark rounded hover:bg-primary-accent1 md:hover:bg-transparent md:border-0 md:hover:text-primary-accent2 md:p-0">
                Home
              </Link>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </header>

  <main>
    <Route path="/">
      <Home
        {products}
        {loading}
        {selectedCategory}
        {sortOrder}
        {filteredProductsList}
        {categories}
        {goToProductDetails}
      />
    </Route>
    <Route path="/product/:id" let:params>
      <ProductDetails productId={params.id} />
    </Route>
  </main>
</Router>

<style>
  body {
    font-family: BDSans-Regular, sans-serif !important;
  }
  * {
    --tw-ring-color: rgba(59, 130, 246, 0.5);
  }
</style>