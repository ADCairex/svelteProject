<script>
	import { db } from "../firebase";
	import {
		collection,
		getDocs,
		doc,
        updateDoc,
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

    let workSelected, workPoints = '';

	let works = [];
    let alumns = [];
	
	const loadWorks = async () => {
		const querySnapshot = await getDocs(collection(db, 'works'));
		let dbWork = [];
		querySnapshot.forEach((doc) => {
			dbWork.push({ ...doc.data(), id: doc.id });
		});
		works = [...dbWork];
	}

    const loadAlumns = async () => {
		const querySnapshot = await getDocs(collection(db, 'alumns'));
		let dbAlumn = [];
		querySnapshot.forEach((doc) => {
			dbAlumn.push({ ...doc.data(), id: doc.id });
		});
		alumns = [...dbAlumn];
		console.log(alumns);
	}

    const evalWork = async (work, points) => {
        await updateDoc(doc(db, 'works', work), {workPoints: points});
        loadAlumns();
        loadWorks();
        success('Trabajo evaluado!')
    }

	loadAlumns();
	loadWorks();
</script>

<main>
    <SvelteToast/>
	<h1>Evaluar trabajos:</h1>
	<div class="addAlumnsContainer">
        <form on:submit|preventDefault={evalWork(workSelected, workPoints)}>
            <label for="workSlect">Seleccionar trabajo:</label>
            <select name="" id="workSelect" bind:value={workSelected}>
                {#each works as i}
                    {#if i.idAlumn != ''}
                        <option value="{i.id}">{i.name}</option>                    
                    {/if}
                {/each}
            </select>
            <label for="alumnSelect">Nota del trabajo:</label>
            <input type="text" bind:value={workPoints}>
            <br>
            <button>Puntuar</button>
        </form>
	</div>
    <div class="assignedWorks">
        {#each works as i}
            {#if i.idAlumn != ''}
                <p>Trabajo: "{i.name}" asignado a 
                {#each alumns as j}
                    {#if j.id == i.idAlumn}
                        {j.name}
                    {/if}
                {/each}
                </p>
            {:else}
                <p>Trabajo: "{i.name}" sin asignar</p>
            {/if}
        {/each}
    </div>
</main>

<style>
</style>