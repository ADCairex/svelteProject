<script>
	import { db } from "./firebase";
	import {
		collection,
		getDocs,
		doc,
		addDoc,
		updateDoc,
		deleteDoc,
	} from "firebase/firestore";

	let alumn = {
		name: '',
		course: '',
		subject: '',
		idWork: '',
	}

	let alumns = [];

	const loadAlumns = async () => {
		const querySnapshot = await getDocs(collection(db, 'alumns'));
		let dbAlumn = [];
		querySnapshot.forEach((doc) => {
			doc.push({ ...doc.data(), id: doc.idAlumn });
		});
		alumns = [...dbAlumn];
		console.log(alumns);
	}
	//loadAlumns();

	const onAlumnSubmitHandler = async (e) => {
		await addDoc(collection(db, 'alumns'), alumn);
		await loadAlumns();
	}
</script>

<main>
	<div class="addAlumnsContainer">
		{#each alumns as i}
			<div>
				<p>{i.name}</p>
			</div>
		{/each}
	</div>
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
</main>

<style>
</style>