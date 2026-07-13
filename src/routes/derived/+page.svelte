<script lang="ts">
	// Nome Sobrenome
	let name = $state('Adadezer');
	let fullName = $derived(name + ' ' + 'Iwazaki');

	// Soma
	let price = $state(350);
	let quantity = $state(2);
	let total = $derived(price * quantity);

	// Desconto
	let subtotal = $state(1000);
	let discount = $state(15);
	let finalPrice = $derived(subtotal * (1 - discount / 100));

	// Filtro de pesquisa
	let search = $state('');
	let products = $state(['Notebook', 'Mouse', 'Monitor', 'Teclado']);
	let filteredProducts = $derived(
		products.filter((product) => product.toLowerCase().includes(search.toLowerCase()))
	);

	// Carrinho de compras
	let cart = $state([
		{ name: 'Mouse', price: 120, quantity: 2 },
		{ name: 'Monitor', price: 900, quantity: 1 }
	]);

	let totalCart = $derived(cart.reduce((acc, item) => acc + item.price * item.quantity, 0));

	// Pode enviar?
	let email = $state('');
	let password = $state('');

	let canSubmit = $derived(email.length > 5 && password.length >= 8);
</script>

<div class="fullName">
	<h2>Nome e sobrenome:</h2>
	<h3>{fullName}</h3>
</div>

<h1>Meus exemplos</h1>
<div class="myExamples">
	<div class="example">
		<h2>Exemplo 1 - Soma</h2>
		<p>Preço: R$ {price}</p>

		<div class="quantity">
			<label for="quantity-input">Quantidade:</label>
			<input id="quantity-input" type="number" min="0" bind:value={quantity} />
		</div>
		<p>Total: R$ {total}</p>
	</div>

	<div class="example">
		<h2>Exemplo 2 - Desconto</h2>
		<p>Subtotal: R$ {subtotal}</p>

		<div class="quantity">
			<label for="discount-input">Desconto (%):</label>
			<input id="discount-input" type="number" min="0" max="100" bind:value={discount} />
		</div>
		<p>Preço final: R$ {finalPrice}</p>
	</div>

	<div class="example">
		<h2>Exemplo 3 - Filtro de pesquisa</h2>

		<div class="quantity">
			<label for="search-input">pesquise o produto:</label>
			<input id="search-input" bind:value={search} />
		</div>
		{#each filteredProducts as product}
			<p>{product}</p>
		{/each}
	</div>

	<div class="example">
		<h2>Exemplo 4 - Carrinho de compras</h2>

		{#each cart as item}
			<div class="cart-item">
				<p>Nome: {item.name}</p>
				<p>Preço: R$ {item.price}</p>
				<input id="quantity-input" type="number" min="0" bind:value={item.quantity} />
			</div>
		{/each}
		<p>Total do carrinho: R$ {totalCart}</p>
	</div>

	<div class="example">
		<h2>Exemplo 5 - Pode enviar?</h2>
		<div class="email-password">
			<div>
				<label for="email-input">email:</label>
				<input id="email-input" bind:value={email} />
			</div>

			<div>
				<label for="password-input">senha:</label>
				<input id="password-input" bind:value={password} />
			</div>
		</div>

		<button disabled={!canSubmit}> Enviar </button>
	</div>
</div>

<style>
	.fullName {
		display: flex;
		align-items: center;
		gap: 1rem;
	}

	.myExamples {
		display: flex;
		gap: 1rem;
	}

	.example {
		display: flex;
		flex-direction: column;
		padding: 0 10px;
		background-color: #ff5820;
		max-width: fit-content;
		border-radius: 10px;
	}

	#quantity-input,
	#discount-input {
		width: 50px;
	}

	#search-input {
		width: 15 0px;
	}

	.email-password {
		display: flex;
		flex-direction: column;
		gap: 15px;
		padding-bottom: 25px;
	}
</style>
