<template lang="pug">
    div
        <br>
        span По площади
        <br>
        input(type="text" name="from" placeholder="От" required :value="from" v-on:input="$emit('input', {val: $event.target.value, id:'from'})")
        <br>
        input(type="text" name="to" placeholder="До" required :value="to" @keyup.delete="$emit('keyNum')" @input="$emit('input', {val: $event.target.value, id:'to'})")
</template>
<script>
export default {
    name: 'field_ploschad',
    props: {
        from: Number,
        to: Number
    }
}
</script>