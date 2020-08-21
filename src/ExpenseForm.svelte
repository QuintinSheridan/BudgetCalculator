<script>
    import {onMount, onDestroy, beforeUpdate, afterUpdate} from 'svelte'

    onMount(() => {
        console.log("form has mounted")
    })
    onDestroy(() => {
        console.log("form is hidden")
    })
    beforeUpdate(() => {
        console.count("before updadte")
    })
    afterUpdate(() => {
        console.count("after update")
    })

    import Title from './Title.svelte'
    export let name = '';
    export let amount = null;
    export let addExpense;
    export let isEditing;
    export let editEpense;
    export let hideForm;
    // reactive variables
    $: formEmpty = !name || !amount;
    // functions
    const handleSubmit = () => {
        // console.log({name, amount})
        if(isEditing) {
            editEpense({name, amount});
            isEditing = false;
        } else {
            addExpense({name, amount});
        }
        name = '';
        amount = null;
    }
</script>

<section class="form">
    <Title title="add expense" />
    <form class="expense-form" on:submit|preventDefault={handleSubmit}>
        <div class="form-control">
            <label for="name">name</label>
            <input type="text" id="name" bind:value={name}>
        </div>
        <div class="form-control">
            <label for="amount">amount</label>
            <input type="number" id="amount" bind:value={amount}>
        </div>
        {#if formEmpty}
            <p class="form-empty">
                Please fill out all form fields.
            </p>
        {/if}
        <button type="submit" class="btn btn-block" class:disabled={formEmpty} disabled={formEmpty}>
            {#if isEditing} Edit Expense{:else} Add Expense{/if}
        </button>
        <button type="button" class="close-btn" on:click={() => hideForm()}>
            <i class="fas fa-times">Close</i>
        </button>
        

    </form>
</section>
