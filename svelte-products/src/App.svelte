<script>
    import { onMount } from 'svelte';
    import Product from './Product.svelte'
    import { total } from './stores.js'

  let products = [];

  onMount(async () => {
    const res = await fetch(`https://makeup-api.herokuapp.com/api/v1/products.json?brand=maybelline`);
    products = await res.json();
        products.forEach(function (element) {
        element.quantity = 5;
        });
    });
        
</script>

<h1>Products</h1>
    {#if products && products.length}
        <div class="photos">
        {#each products as product}
                <Product product={product} />
            {/each}
    </div>    
  {:else}
    <p>loading...</p>
  {/if}
   
<div>
    <h1>Total {$total.toFixed(2)}</h1>
</div>

<style>
    .photos {
        width: 100%;
        display: grid;
        grid-template-columns: repeat(5, 1fr);
        grid-gap: 8px;
    }

   
</style> 