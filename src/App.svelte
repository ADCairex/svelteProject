<script>
	import { Router, Route, Link } from 'svelte-routing';
	import Index from './pages/index.svelte';
	import Alumns from './pages/alumns.svelte';
	import Works from './pages/works.svelte';
	import AssignWorks from './pages/assignWorks.svelte'
	import EvaluateWorks from './pages/evaluateWorks.svelte'
	export let url = '';
</script>
<main>
	<Router url='{ url }'>
		<h3>Menu de navegacion</h3>
		<nav>
			<Link to='/'>Inicio</Link>
			<Link to='/alumns'>Alumnos</Link>
			<Link to='/works'>Trabajos</Link>
			<Link to='/assignWorks'>Asignar trabajos</Link>
			<Link to='/evaluateWorks'>Evaluar trabajos</Link>
		</nav>
		<div>
			<Route path='/'><Index /></Route>
			<Route path='/works'><Works /></Route>
			<Route path='/alumns'><Alumns /></Route>
			<Route path='/assignWorks'><AssignWorks /></Route>
			<Route path='/evaluateWorks'><EvaluateWorks /></Route>
		</div>
	</Router>
</main>