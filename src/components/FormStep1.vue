<script setup lang="ts"></script>

<template>
    <fieldset>
        <legend>Personal info</legend>
        <p>Please provide your name, email address, and phone number.</p>

        <label for="name">Name</label>
        <input class="form-control" type="text" name="name" id="name" placeholder="e.g. Stephen King">

        <label for="email">Email Address</label>
        <input class="form-control" type="email" name="email" id="email" placeholder="e.g. stephenking@lorem.com">

        <label for="phone">Phone Number</label>
        <input class="form-control" type="tel" name="phone" id="phone" placeholder="e.g. +1 234 567 890">
    </fieldset>
</template>

<style scoped>
.form-control {
    display: block;
    width: 100%;

    padding: .7em;
    margin: 2% 0 5% 0;

    border: 1px solid var(--Light-gray);
    border-radius: 7px;
}
</style>