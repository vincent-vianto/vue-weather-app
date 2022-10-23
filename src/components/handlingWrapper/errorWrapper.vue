<template>
    <div className="errorWrapper">
        <h1>{{errorMsg.cod}}</h1>
        <h2>{{errorMsg.message}}</h2>
    </div>
</template>
  
<script>


export default {
    name: 'ErrorWrapper',
    props: {
        errorMsg: {}
    },
}
</script>
  
  