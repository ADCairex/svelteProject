<script>

	let alumn = {
		name: '',
		course: '',
		subject: '',
		idWork: '',
	}

	const onAlumnSubmitHandler = (e) => {
		console.log(alumn);
	}
</script>

<main>
	<div class="addAlumnsContainer">
		<h2>Agregar nuevo usuario:</h2>
		<form on:submit|preventDefault={onAlumnSubmitHandler}>
			<label for="alumnName">Nombre del alumno:</label>
			<input 
				bind:value={alumn.name}
				type="text"
				id="alumnName"
				placeholder="Nombre"
			/>
			<label for="alumnCourse">Curso al que pertenece el alumno</label>
			<input
				type="text"
				bind:value={alumn.course}
				id="alumnCourse"
				placeholder="Curso"
			/>
			<button>Agregar</button>
		</form>
	</div>
</main>

<style>
</style>