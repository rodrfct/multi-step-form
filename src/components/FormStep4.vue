<script setup lang="ts"></script>

<template>
    <fieldset>
        <legend>Finishing up</legend>
        <p>Double-check everything looks OK before confirming.</p>

        <div class="summary">
            <div class="item plan">
                <div class="selection">
                    <span>Arcade (Monthly)</span>
                    <p @click="$emit('select-step', 2)">Change</p>
                </div>

                <span class="price">$9/mo</span>
            </div>
            <div class="item">
                <p>Online service</p>
                <span class="price">+$1/mo</span>
            </div>
            <div class="item">
                <p>Larger storage</p>
                <span class="price">+$2/mo</span>
            </div>
        </div>

        <div class="item total">
            <p>Total (per month)</p>

            <span class="price">+$12/mo</span>
        </div>
    </fieldset>
</template>

<style scoped>
.summary {
    background-color: var(--Magnolia);
    padding: 15px 0;
    margin-top: 10%;
}

.item {
    display: flex;
    justify-content: space-between;
    align-items: center;

    margin: 2% 6%;
}

.item p {
    margin: 2% 0;
}

.plan {
    border-bottom: 2px solid var(--Light-gray);
}

.plan > span {
    font-weight: 500;
}

.plan > * {
    margin-bottom: 7%;
}

.selection span {
    font-weight: 500;
}

.selection p {
    margin: 5px 0 0 0;
    text-decoration: underline;
    cursor: pointer;
}

.total {
    margin-top: 5%;
}

.total span {
    color: var(--Purplish-blue);
    font-weight: 700;
    font-size: 1.1em;
}
</style>