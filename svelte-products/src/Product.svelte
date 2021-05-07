<script>
    import { total } from './stores.js';
    export let product;

    function increment(price) {
        $total = $total + price;
        product.quantity = product.quantity - 1;
    }

    function decrement(price) {
        $total = $total - price;
        product.quantity = product.quantity + 1;
    }

</script>

<figure>
    <img src={product.image_link} alt={product.name} />
    <figcaption>{product.name}</figcaption>
    <small
        >£{product.price}<small />
        <h1>Quantity: {product.quantity}</h1>
        {#if product.quantity === 0}  <!-- disable button if quantity is max or minimum -->
        <button disabled>+</button>
        {:else}
        <button on:click={increment(parseFloat(product.price))}>+</button>  <!-- the api returns the price as string, parsefloat converts the string to float -->
        {/if}

        {#if product.quantity === 5}
        <button disabled >-</button>
        {:else}
        <button on:click={decrement(parseFloat(product.price))}>-</button>
        {/if}
    </small>
</figure>

<style>
    figure,
    img {
        width: 100%;
        margin: 0;
    }
</style>