<template lang="pug">
    i.fas.fa-filter(@click="$emit('sortBlock')")
</template>
<script>

export default {
    name: 'navigatePanel'
}
</script>
<style lang="scss" scoped>
    i {
        cursor: pointer;
    }
</style>