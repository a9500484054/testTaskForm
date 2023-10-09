<template>
    <div class="progress">
        <div class="progress-bar" role="progressbar" aria-label="Basic example" style="width: 25%" aria-valuenow="25" aria-valuemin="0" aria-valuemax="100">
            <slot></slot>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'my-bar'
    }
</script>

<style scoped>

</style>