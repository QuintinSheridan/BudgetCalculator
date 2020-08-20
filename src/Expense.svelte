<script>
    // import context to receive access to functions defined in parent  elements
    import {getContext, createEventDispatcher} from 'svelte'
    // exports
    export let id;
    export let name;
    export let amount;
    // export let removeExpense;
    let displayAmount = false;
    // functions
    const toggleDisplayAmount = () => displayAmount=!displayAmount
    const state = getContext('state')
    const removeExpense = state.remove

    const dispatch = createEventDispatcher()
</script>

<article class="single-expense">
    <div class="expense-info">
        <h2>{name} 
            <button class="amount-btn" on:click={toggleDisplayAmount}>
                <i class="fas fa-caret-down"></i>
            </button>
        </h2>
        <!-- display amount if button is clicked -->
            {#if displayAmount}
                <h4>
                    Amount: ${amount}
                </h4>
            {/if}
    </div>
    <div class="expense-button">
        <button class="expense-btn edit-btn">
            <i class="fas fa-pen"></i>
        </button>
        <button class="expense-btn delete-btn" on:click={() => removeExpense(id)}>
            <i class="fas fa-trash"></i>
        </button>
    </div>

</article>
