<!-- JS -->
<script>
	import {setContext} from "svelte"
	// components
	import Navbar from './Navbar.svelte'
	import ExpensesList from './ExpensesList.svelte'
	import Totals from './Totals.svelte'
	// data
	import expensesData from './expenses'
	// variables
	let expenses = [...expensesData]
	// reactive
	$: total = expenses.reduce((acc, current) => acc+=current.amount, 0)
	// console.log(expenses)
	// functions
	const removeExpense = (id) => {
		expenses = expenses.filter((expense) => expense.id !== id)
	}

	const clearExpenses = () => {
		expenses=[]
	}

	// context - allows child elements to access function
	const state = {
		name: 'simple name',
		remove: removeExpense
	}
	setContext('state', state);
</script>
<!-- CSS -->


<!-- HTML -->
<Navbar />

<main class="content">
	<Totals title="total expenses" {total} />
	<ExpensesList {expenses} />
	<button type="button" class="btn btn-primary btn-block" on:click={clearExpenses}>Clear Expenses</button>
</main>

