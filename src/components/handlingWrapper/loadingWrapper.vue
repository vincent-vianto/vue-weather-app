<template>
    <div class="loaderWrapper">
        <MoonLoader color="white" />
        <div class="mt-5 d-inline-flex flex-row">
            <h3>Loading</h3>
        </div>
    </div>
</template>
  
<script>

import MoonLoader from 'vue-spinner/src/MoonLoader.vue'

export default {
    name: 'LoadingWrapper',
    components: { MoonLoader },

    props: {
        errorMsg: {}
    },
}
</script>