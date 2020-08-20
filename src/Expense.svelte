<script>
    // export let index;
    export let id;
    export let name;
    export let amount;
</script>
<!-- <div>
    <!-- <p>{index}</p> -->
    <!-- <h2>{name} - {amount} </h2>
</div> --> -->

<article class="single-expense">
    <div class="expense-info">
        <h2>{name} 
            <button class="amount-btn">
                <i class="fas fa-caret-down"></i>
            </button>
        </h2>
        <h4>
            Amount: ${amount}
        </h4>
    </div>
    <div class="expense-button">
        <button class="expense-btn edit-btn">
            <i class="fas fa-pen"></i>
        </button>
        <button class="expense-btn delete-btn">
            <i class="fas fa-trash"></i>
        </button>
    </div>

</article>
