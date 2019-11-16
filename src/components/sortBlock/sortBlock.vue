<template lang="pug">
    .vue-table__sort
        <select v-bind:value="column" v-on:input="$emit('input', {id:$event.target.value})" v-model="visible">
            <option selected="selected" disabled value="">Вид сортировки</option>
            <option value="field_stoimost">По цене</option>
            <option value="field_ploschad">По площади</option>
            //<option value="status">Статус</option>
            <option value="field_telefon_prodavca">Телефон Продавца</option>
            <option value="field_kol_komnat">Комнат</option>
            <option value="field_ploschad_kukhni">Площадь кухни</option>
            <option value="field_ploschad_zhilaya">Жилая площадь</option>
            <option value="field_fio">Менеджер</option>
            <option value="field_rayon">Район</option>
        </select>
        <br>
        component(:is="visible" v-model="message" @input="$emit('input', message)" @keyNum="$emit('keyNumSort')")
        
</template>
<script>
import field_stoimost from './field_stoimost.vue'
import field_ploschad from './field_ploschad.vue'
//import status from './status.vue'
import field_telefon_prodavca from './field_telefon_prodavca.vue'
import field_kol_komnat from './field_kol_komnat.vue'
import field_ploschad_kukhni from './field_ploschad_kukhni.vue'
import field_ploschad_zhilaya from './field_ploschad_zhilaya.vue'
import field_fio from './field_fio.vue'
import field_rayon from './field_rayon.vue'

export default {
    name: 'sortBlock',
    props: {
        column: String
    },
    data(){
        return {
            visible:'',
            message:''
        }
    },
    methods: {
        visibleSortComponent() {
            return this.visible
        },
    },
    components: {
        field_stoimost,
        field_ploschad,
        //status,
        field_telefon_prodavca,
        field_kol_komnat,
        field_ploschad_kukhni,
        field_ploschad_zhilaya,
        field_fio,
        field_rayon
    }
}
</script>