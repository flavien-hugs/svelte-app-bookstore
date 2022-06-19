<script>
    import { createEventDispatcher } from 'svelte'
    import Button from './Button.svelte'

    export let bookTitle;
    export let bookAuthor;
    export let bookPrice;
    export let BookDescription;

    const dispatch = createEventDispatcher()

    const purchaseBook = () => {
        dispatch("buy", bookTitle)
    }
</script>


<div>
    <h2>{bookTitle} de <em>{bookAuthor}</em></h2>
    <p>{bookPrice}</p>
    <p>{BookDescription}</p>
    <Button on:click={purchaseBook}>Buy Book</Button>
</div>

<style>
    div {
        margin: 1rem;
        padding: 1rem;
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26)
    }
    h2 {
        font-size: 1rem;
        margin: 0.25rem 0;
        color: aqua;
        font-weight: bold;
    }
    p {
        margin: 0.25rem 0;
    }
</style>
