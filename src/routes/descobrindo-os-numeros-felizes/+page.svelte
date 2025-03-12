<script lang="ts">
	// Solução original - Sem auxilio de IA
	function initialSolution(e: Event) {
		e.preventDefault();
		const form = e.target as HTMLFormElement;
		const formData = new FormData(form);
		const valueStr = formData.get('numberToCheck') as string;
		const valueNum = parseFloat(valueStr);

		// Lista com alguns loops conhecidos
		const knownLoops = [4, 16, 37, 58, 89, 145, 42, 20];

		// Verifica se os números atende a regra básica de ser um interio = ou > que 1
		if (!Number.isInteger(valueNum) || valueNum < 1) {
			return alert('Esse número é triste!');
		}

		// Função que converte o valor recebido em um array de números sem zeros
		function arrGenerator(value: number) {
			return String(value)
				.split('')
				.map(Number)
				.filter((value) => Number(value) !== 0);
		}

		// Função que executa o calculo para identificar o número feliz
		function happyCalc(value: number) {
			const arr = arrGenerator(value);
			const squares = arr.map((value) => value * value);
			return squares.reduce((acc, curr) => acc + curr, 0);
		}

		let result = happyCalc(valueNum);
		let resultList = [result];

		do {
			if (knownLoops.includes(result)) return alert('Esse número é triste!');
			if (resultList.length !== new Set(resultList).size) return alert('Esse número é triste!');

			result = happyCalc(result);
			resultList.push(result);
		} while (result !== 1);

		return alert('Esse é um número feliz!');
	}

	// Solução revisada pelo ChatGPT
	function formHandler(e: Event) {
		e.preventDefault();
		const form = e.target as HTMLFormElement;
		const formData = new FormData(form);
		const valueStr = formData.get('numberToCheck') as string;
		const valueNum = parseFloat(valueStr);

		// Lista com alguns loops conhecidos
		const knownLoops = [4, 16, 37, 58, 89, 145, 42, 20];

		// Verifica se os números atende a regra básica de ser um interio = ou > que 1
		if (!Number.isInteger(valueNum) || valueNum < 1) {
			return alert('Esse número é triste!');
		}

		// Função que executa o calculo para identificar o número feliz
		function happyCalc(value: number) {
			return String(value)
				.split('')
				.reduce((acc, digit) => acc + Math.pow(Number(digit), 2), 0);
		}

		let result = happyCalc(valueNum);
		let resultList = new Set([result]);

		do {
			if (knownLoops.includes(result)) return alert('Esse número é triste!');
			if (resultList.has(result)) return alert('Esse número é triste!');

			result = happyCalc(result);
			resultList.add(result);
		} while (result !== 1);

		return alert('Esse é um número feliz!');
	}
</script>

<h1>Descobrindo os números felizes</h1>

<form onsubmit={formHandler}>
	<label for="numberToCheck">
		Número para chechar:
		<input type="number" name="numberToCheck" placeholder="37" required />
	</label>

	<button>Checar se é feliz</button>
</form>
