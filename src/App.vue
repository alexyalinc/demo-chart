<template>
    <div>
        <Promotion />
    </div>
</template>

<script>
import Promotion from "./components/Promotion"
export default {
    name: "App",
    components: {
      Promotion
    },
};
</script>

<style>
* {
  box-sizing: border-box;
}
html {
    /* 1rem = 10px */
    font-size: 62.5%;
    width: 100%;
}
body {
    width: 100%;
    font-size: 1.6rem;
    font-family: 'PT Sans', sans-serif;

    /* colors */
    --black-main: #212121; 
    --grey-body-landing: #505361; 
    --black-minor: #717171; 
    --grey-minor: #E2E5EE; 
    --white-main: #FFFFFF; 
    --violet-lilac: #BC9AF4; 
    --violet-lilac-opacity: rgba(188, 154, 244, .3); 
    margin: 0;
}
</style>

<style scoped>

</style>