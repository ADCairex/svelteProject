<script>

	let alumn = {
		name: '',
		course: '',
		subject: '',
		idWork: '',
	}

	const onAlumnSubmitHandler = (e) => {

	}
</script>

<main>
	<div class="alumnsContainer">
		<form on:submit|preventDefault={onAlumnSubmitHandler}>
			<label for="alumnName">Nombre del alumno:</label>
			<input 
				bind:value={alumn.name}
				type="text"
				id="alumnName"
				placeholder="Nombre"
			/>
		</form>
	</div>
</main>

<style>
</style>