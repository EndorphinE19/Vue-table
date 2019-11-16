<template lang="pug">
    div
        <br>
        span Район
        <br>
        input(type="text" name="vals" placeholder="Значение" required :value="vals" v-on:input="$emit('input', {val: $event.target.value, id:'val'})")
</template>
<script>
export default {
    name: 'field_rayon',
    props: {
        vals: String
    }
}
</script>