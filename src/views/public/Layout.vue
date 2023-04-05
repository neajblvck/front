<script>

import testComponent from '@/components/testComponent.vue';
import PublicNav from '@/components/PublicNav.vue'
import NavMobile from '@/components/NavMobile'
import BurgerNav from '@/components/BurgerNav.vue';
import NewdeliceNav from '../../components/newdeliceNav.vue';

export default{
    name: 'PublicLayout',
    components: {
    PublicNav,
    NavMobile,
    BurgerNav,
    testComponent,
    NewdeliceNav
}

}

</script>

<template>
    <div id="public">
        <PublicNav/>
        <!-- <BurgerNav/> -->
        <!-- <testComponent/> -->
        <NewdeliceNav/>

        <router-view/> 
    </div> 
</template>

