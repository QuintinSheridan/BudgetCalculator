<!-- JS -->
<script>
	import {setContext, onMount} from "svelte"

	localStorage.setItem("testing", "hello")
	// components
	import Navbar from './Navbar.svelte'
	import ExpensesList from './ExpensesList.svelte'
	import Totals from './Totals.svelte'
	import ExpenseForm from './ExpenseForm.svelte'
	// data
	// import expensesData from './expenses'
	import Expense from "./Expense.svelte";
	// variables
	// let expenses = [...expensesData]
	let expenses = []
	let setId = ''
	let setName = null;
	let setAmount = null;
	// toggle form variables
	let isFormOpen = false;
	// reactive
	$: isEditing = setId? true:false;
	$: total = expenses.reduce((acc, current) => acc+=current.amount, 0);
	// functions
	const showForm = () => {
		isFormOpen = true;
	}

	const hideForm = () => {
		isFormOpen =false;
	}

	const removeExpense = (id) => {
		expenses = expenses.filter((expense) => expense.id !== id);
		setLocalStorage();
	}

	const clearExpenses = () => {
		expenses=[];
		setLocalStorage();
	}

	const addExpense = ({name, amount}) => {
		console.log(name, amount)
		let expense = {
			id: Math.random()*Date.now(),
			name,
			amount
		}
		expenses = [expense, ...expenses]
		setLocalStorage();
	}

	const setModifiedExpense = (id) => {
		let expense = expenses.find(expense => expense.id===id)
		
		setId = expense.id;
		setName = expense.name;
		setAmount = expense.amount;
		showForm()
	}

	const editEpense = ({name, amount}) => {
		expenses = expenses.map(expense => {
			return expense.id === setId? {id:setId, name, amount}: expense
		})

		setId = null;
		setName = '';
		setAmount = null
		setLocalStorage();
	}

	// context - allows child elements to access function
	const state = {
		name: 'simple name',
		remove: removeExpense,
		modify: setModifiedExpense
	}
	setContext('state', state);

	// local storage
	const setLocalStorage = () => {
		localStorage.setItem('expenses', JSON.stringify(expenses));
	}

	onMount(() => {
		expenses =  localStorage.getItem('expenses')? 
			JSON.parse(localStorage.getItem('expenses')):[];
	})

</script>
<!-- CSS -->


<!-- HTML -->
<Navbar {showForm}/>

<main class="content">
	{#if isFormOpen}
		<ExpenseForm {addExpense} name={setName} amount={setAmount} {isEditing} {editEpense} {hideForm}/>
	{/if}
	<Totals title="total expenses" {total} />
	<ExpensesList {expenses} />
	<button type="button" class="btn btn-primary btn-block" on:click={clearExpenses}>Clear Expenses</button>
</main>

