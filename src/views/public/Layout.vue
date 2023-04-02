<template>
    <div id="public">
        <PublicNav/>
        <!-- <sideNav/> -->
        <router-view/> 
    </div> 
</template>

<script>

import PublicNav from '@/components/PublicNav.vue'
import sideNav from '@/components/sideNav.vue';

export default{
    name: 'PublicLayout',
    components: {
        PublicNav,
        sideNav
    }

}

</script>

<style>

#public{
    position: relative;
    display: flex;
    flex-direction: column;
    text-align: center;
    padding-top: 80px;
    padding-bottom: 40px;
    background-color: #1a8737;
}

@media screen and (max-width: 650px){

.navbar{
    display: none;
}
#public{
    padding-top: 0;
}
}



/* .link{
    color: white;
    text-decoration: none;
} */

</style> 