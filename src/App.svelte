<script>
	import { Router, Route, Link } from 'svelte-routing';
	import Alumns from './pages/alumns.svelte';
	import Works from './pages/works.svelte';
	export let url = '';
</script>
<main>
	<Router url='url'>
		<h1>Pagina de inicio</h1>
		<nav>
			<Link to='/alumns'>Alumnos</Link>
			<Link to='/works'>Trabajos</Link>
		</nav>
		<div>
			<Route path='/works'><Works /></Route>
			<Route path='/alumns'><Alumns /></Route>
		</div>
	</Router>
</main>
<style>

</style>