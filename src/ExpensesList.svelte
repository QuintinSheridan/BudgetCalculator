<script>
    import SectionTitle from './Title.svelte'
    import Expense from './Expense.svelte'
    export let expenses = [];
    // export let removeExpense;
</script>

<style>
    h2 {
        text-transform: capitalize;
    }
</style>

<section>
    <SectionTitle title="Expense List"/>
    <ul>
        {#each expenses as expense, index}
            <Expense {...expense}/>
            {:else}
            <h2>Currently you have no expenses</h2>
        {/each}
    </ul>
</section>