<template>
    <header class="main-header">
        <img class= "image-logo image-logo__abba" src="../../public/logo-nuevo-abba.png" alt="Logo abba seguros">
        <img class= "image-logo image-logo__sura" src="../../public/logo-sura-financia.png" alt="Logo sura">
    </header>
</template>

<style scoped>
.main-header{
    width: 100%;
    position: fixed;
    top: 0;
    left: 0;
    background: #ffffff;
    padding: 0.5rem 1rem;
    z-index : 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    box-shadow: 3px 3px 3px 3px rgba(0, 0, 0, 0.16);
}

.image-logo__abba {
    height: 2.8rem;
}

.image-logo__sura {
    height: 2.5rem;
}


@media (min-width: 22rem){
.main-header{
   flex-direction: row;
}

.image-logo__abba {
    height: 3.6rem;
}

.image-logo__sura {
    height: 3.3rem;
    padding-top: 7px;
}

}

</style>