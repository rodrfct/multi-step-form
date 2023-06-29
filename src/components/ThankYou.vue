<template>
    <div class="thank-you">
        <img src="../assets/icons/icon-thank-you.svg" alt="">

        <span>Thank You!</span>

        <p>Thanks for confirming your subscription! We hope you have fun using our platform. If you ever need support, please feel free to email us at support@loremgaming.com.</p>
    </div>
</template>

<style scoped>
.thank-you {
    margin: 0 13%;
    padding: 25% 0;
    color: var(--Marine-blue);
    text-align: center;
}

.thank-you img {
    display: block;
    margin: 0 auto 10% auto;
}

.thank-you span {
    font-size: 1.75em;
    font-weight: 700;
}

.thank-you p {
    color: var(--Cool-gray);
}

@media (width < 400px) {
    .thank-you {
        position: absolute;
        top: 16%;

        margin: 0 5%;
        padding: 40px 20px 20px 20px;

        background-color: var(--Alabaster);
        border-radius: 15px;

        box-shadow: -1px 1px 4px #999;
    }

    .thank-you img {
        width: 60px;
        margin: 0 auto 7% auto;
    }
}
</style>