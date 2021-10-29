<script>
	import { db } from "../firebase";
	import {
		collection,
		getDocs,
		doc,
		addDoc,
		updateDoc,
		deleteDoc,
	} from "firebase/firestore";
    export let url = '/alumns';

	let alumn = {
		name: '',
		course: '',
		idWork: '',
	}

	let alumns = [];
	
	const loadAlumns = async () => {
		const querySnapshot = await getDocs(collection(db, 'alumns'));
		let dbAlumn = [];
		querySnapshot.forEach((doc) => {
			dbAlumn.push({ ...doc.data(), id: doc.id });
		});
		alumns = [...dbAlumn];
		console.log(alumns);
	}
	loadAlumns();

	const onAlumnSubmitHandler = async (e) => {
		await addDoc(collection(db, 'alumns'), alumn);
		await loadAlumns();
	}
</script>

<main>
	<h1>Agregar nuevo usuario:</h1>
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
	<h2>Lista de alumnos:</h2>
	<div class="addAlumnsContainer">
		{#each alumns as i}
			<div>
				<p>Nombre: {i.name}</p>
				<p>Curso: {i.course}</p>
				{#if i.idWork == ''}
					<p>Trabajo: Sin asignar</p>
				{:else}
					<p>Trabajo: {i.idWork}</p>
				{/if}
			</div>
			<br>
		{/each}
	</div>
</main>

<style>
</style>