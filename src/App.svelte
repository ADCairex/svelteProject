<script>
	import { Router, Route, Link } from 'svelte-routing';
	import Alumns from './pages/alumns.svelte';
	import Works from './pages/works.svelte';
	import AssignWorks from './pages/assignWorks.svelte'
	import EvaluateWorks from './pages/evaluateWorks.svelte'
	export let url = '';
</script>
<main>
	<Router url='{ url }'>
		<h1>Menu de navegacion</h1>
		<nav>
			<Link to='/alumns'>Alumnos</Link>
			<Link to='/works'>Trabajos</Link>
			<Link to='/assignWorks'>Asignar trabajos</Link>
			<Link to='/evaluateWorks'>Evaluar trabajos</Link>
		</nav>
		<div>
			<Route path='/works'><Works /></Route>
			<Route path='/alumns'><Alumns /></Route>
			<Route path='/assignWorks'><AssignWorks /></Route>
			<Route path='/evaluateWorks'><EvaluateWorks /></Route>
		</div>
	</Router>
</main>
<style>

</style>