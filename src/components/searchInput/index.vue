<template>
    <div>
        <form @submit="handleSubmit">
            <div class="input-group" >
                <input type="text" placeholder="Search city's weather here" @change="handleChange"
                    class="form-control bg-transparent text-light formSearchBox" />
                <button variant="transparent" 
                    class="btn btn-outline-secondary text-light formButton" type="submit">
                    Search
                </button>
            </div>
        </form>
    </div>
</template>
  
<script>
import './style.css'
export default {
    name: 'searchInput',
    props: ['handleSubmit', 'query', 'handleChange']
}
</script>
