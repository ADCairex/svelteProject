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
	import { SvelteToast } from '@zerodevx/svelte-toast';
	import { toast } from '@zerodevx/svelte-toast';

	//Def the succes toast
	const success = m => toast.push(m, {
		theme: {
			'--toastBackground': 'green',
			'--toastColor': 'white',
			'--toastBarBackground': 'olive'
		}
	});

	let work = {
		name: '',
		subject: '',
		idAlumn: '',
	}

	let works = [];
	
	const loadWorks = async () => {
		const querySnapshot = await getDocs(collection(db, 'works'));
		let dbWork = [];
		querySnapshot.forEach((doc) => {
			dbWork.push({ ...doc.data(), id: doc.id });
		});
		works = [...dbWork];
	}
	loadWorks();

	const onAlumnSubmitHandler = async (e) => {
		await addDoc(collection(db, 'works'), work);
		await loadWorks();

		success('Trabajo agregado!');
	}
</script>

<main>
	<SvelteToast/>
	<h1>Agregar nuevo trabajo:</h1>
	<form on:submit|preventDefault={onAlumnSubmitHandler}>
		<label for="workName">Nombre del trabajo:</label>
		<input 
			bind:value={work.name}
			type="text"
			id="workName"
			placeholder="Nombre"
		/>
		<label for="workSubject">Asigunatura del trabajo:</label>
		<input
			type="text"
			bind:value={work.subject}
			id="workSubject"
			placeholder="Asignatura"
		/>
		<button>Agregar</button>
	</form>
	<h2>Lista de trabajos:</h2>
	<div class="addAlumnsContainer">
		{#each works as i}
			<div>
				<p>Nombre: {i.name}</p>
				<p>Curso: {i.subject}</p>
				{#if i.idAlumn == ''}
					<p>Trabajo: Sin alumno asignado</p>
				{:else}
					<p>Trabajo: Asignado</p>
				{/if}
			</div>
			<br>
		{/each}
	</div>
</main>

<style>
</style>