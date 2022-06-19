<script>
	import Book from './components/Book.svelte'
	import Button from './components/Button.svelte'
	import Purchase from './components/Purchase.svelte'

	let title = '';
	let author = '';
	let price = 0;
	let description = '';

	let books = [];
	let purchases = [];

	const setTitle = (event) => {
		title = event.target.value;
	}

	const setAuthor = (event) => {
		author = event.target.value;
	}

	const setDescription = (event) => {
		description = event.target.value;
	}

	const addBook = () => {
		const newBook = {
			title: title,
			author: author,
			price: price,
			description: description
		};
		books = books.concat(newBook)
	}

	const purchaseBook = (event) => {
		const selectedTitle = event.detail;
		purchases = purchases.concat({
			...books.find(book => book.title === selectedTitle)
		});
	}
</script>

<section>
	<h2>Add New Book</h2>
	<div>
		<label for="title">Title</label>
		<input
			type="text"
			id="title"
			value={title}
			on:input={setTitle}
		/>
	</div>

	<div>
		<label for="author">Author</label>
		<input
			type="text"
			id="author"
			value={author}
			on:input={setAuthor}
		/>
	</div>

	<div>
        <label for="price">Price</label>
        <input
			type="number"
			id="price"
			bind:value={price}
		/>
    </div>

	<div>
        <label for="description">Description</label>
        <textarea
			rows="3"
			id="description"
			bind:value={description}
			on:input={setDescription}
		/>
    </div>

	<Button on:click={addBook}>ADD Book</Button>
</section>

<section>
	<h2>Stock</h2>
	{#if books.length === 0}
		<p>No books in stock.</p>
	{:else}
		{#each books as book }
			<Book
				bookTitle={book.title}
				bookAuthor={book.author}
				bookPrice={book.price}
				bookDescription={book.description}
				on:buy={purchaseBook}
			/>
		{/each}
	{/if}
</section>

<section>
	<Purchase books={purchases}/>
</section>

<style>
	section{
        margin: auto;
        width :30rem;
    }
    label, input, textarea{
		width: 100%
	}
</style>
