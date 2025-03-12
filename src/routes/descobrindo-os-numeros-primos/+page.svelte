<script lang="ts">
	function handleForm(e: Event) {
		e.preventDefault();

		const form = e.target as HTMLFormElement;
		const formData = new FormData(form);
		const value = Number(formData.get('numberToCheck'));

		// Por definição um número primo deve ser maior que um
		if (value <= 1) {
			return alert('Não é primo');
		}

		// Verifica se o valor é igual aos dois menores números primos
		if (value === 2 || value === 3) {
			return alert('é primo');
		}

		// Verifica se o número pode ser dividio por 2 ou 3 se sim não é primo
		if (value % 2 === 0 || value % 3 === 0) {
			return alert('Não é primo');
		}

		let sqrt = Math.sqrt(value);

		for (let i = 5; i < Math.ceil(sqrt); i += 6) {
			if (value % i === 0 && value % (i + 2) === 0) {
				return alert('Não é primo');
			}
		}

		return alert('É primo');
	}
</script>

<h1>Descobrindo os números primos</h1>

<form onsubmit={handleForm}>
	<label for="numberToCheck"
		>Número para checar: <input
			type="number"
			name="numberToCheck"
			placeholder="26"
			required
		/></label
	>
	<button>Checar se é primo</button>
</form>
