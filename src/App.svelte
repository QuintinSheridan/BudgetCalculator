<!-- JS -->
<script>
	// components
	import Navbar from './Navbar.svelte'
	import ExpensesList from './ExpensesList.svelte'
	// data
	import expensesData from './expenses'
	// variables
	let expenses = [...expensesData]
	console.log(expenses)
</script>
<!-- CSS -->


<!-- HTML -->
<Navbar />

<main class="content">
	<ExpensesList expenses = {expenses}/>
</main>

