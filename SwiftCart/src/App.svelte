<script>
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
    <!-- {#await renderComponent() then Component}
      <svelte:component this={Component} />
    {/await} -->
  </Layout>
</div>

<style>
  @import './app.css';
</style>