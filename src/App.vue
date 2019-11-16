<template lang="pug">
    #app.vue-table
      .vue-table__navigate-panel
          navigatePanel(@sortBlock="navigateVisible")
          component(:is="componentVisible()" v-bind:class="[visible ? 'showPanel' : 'hidePanel']" v-model.trim="message" @input="messages(message)" @keyNumSort="toAddNumber()")
      .vue-table__body
        .vue-table__head-body
            .vue-table__list
              .vue-table__elem-head(v-for="(item, indx) in dataTitle" :key="item.title")
                  span {{item.title}}
                    i.fas.fa-sort(@click="costFromAndTo()")
        .vue-table__content
          .vue-table__content-body(v-for="obj of dataContent")
            template(v-if="(field === 'field_stoimost') || (field === 'field_ploschad') || (field === 'field_ploschad_kukhni') || (field === 'field_ploschad_zhilaya')")
              .vue-table__content-column(v-if="obj[field].num <= to && obj[field].num >= from")
                  span {{obj.nid}}
                  span {{obj.field_kol_komnat}}
                  span {{obj.field_ploschad.str}}
                  span(v-html="obj.field_polnyy_adres")
                  span {{obj.status}}
                  span {{obj.field_stoimost.str}}
                  span {{obj.field_imya_prodavca}}
                  span {{obj.field_telefon_prodavca}}
                  span {{obj.field_fio}}
                  span {{obj.created}}
                  span {{obj.field_publish_avito}}
                  span {{obj.field_publish_cian}}
                  span {{obj.field_publish_domclick}}
                  span {{obj.field_publish_yandex}}
                  span(v-html="obj.operations")
            template(v-else)
              template(v-if="val.length !== 0")
                .vue-table__content-column(v-if="obj[field] === val")
                    span {{obj.nid}}
                    span {{obj.field_kol_komnat}}
                    span {{obj.field_ploschad.str}}
                    span(v-html="obj.field_polnyy_adres")
                    span {{obj.status}}
                    span {{obj.field_stoimost.str}}
                    span {{obj.field_imya_prodavca}}
                    span {{obj.field_telefon_prodavca}}
                    span {{obj.field_fio}}
                    span {{obj.created}}
                    span {{obj.field_publish_avito}}
                    span {{obj.field_publish_cian}}
                    span {{obj.field_publish_domclick}}
                    span {{obj.field_publish_yandex}}
                    span(v-html="obj.operations")
              .vue-table__content-column(v-else)
                    span {{obj.nid}}
                    span {{obj.field_kol_komnat}}
                    span {{obj.field_ploschad.str}}
                    span(v-html="obj.field_polnyy_adres")
                    span {{obj.status}}
                    span {{obj.field_stoimost.str}}
                    span {{obj.field_imya_prodavca}}
                    span {{obj.field_telefon_prodavca}}
                    span {{obj.field_fio}}
                    span {{obj.created}}
                    span {{obj.field_publish_avito}}
                    span {{obj.field_publish_cian}}
                    span {{obj.field_publish_domclick}}
                    span {{obj.field_publish_yandex}}
                    span(v-html="obj.operations")
              
</template>

<script>
import navigatePanel from '@/components/navigatePanel.vue';
import sortBlock from '@/components/sortBlock/sortBlock.vue';
import { setTimeout } from 'timers';
export default {
  
  mounted: function() {

    this.fetchData()
    this.componentVisible()
    
  },
  components: {
    navigatePanel,
    sortBlock
  },
  data() {
    return {
      field:'',
      message:'',
      val:'',
      from:0,
      to:10000000,
      visible: false,
      dataTitle: [
        {title: '№'},
        {title: 'Комнат'},
        {title: 'Площадь'},
        {title: 'Ссылка'},
        {title: 'Статус'},
        {title: 'Стоимость'},
        {title: 'Имя продавца'},
        {title: 'Телефон продавца'},
        {title: 'Имя менеджера'},
        {title: 'Создано'},
        {title: 'Авито'},
        {title: 'ЦИАН'},
        {title: 'ДомКлик'},
        {title: 'Yandex'},
        {title: 'Операции'}
      ],
      dataContent: []
    }
  },
  methods: {
    fetchData() {

      fetch('http://renevada.ru/1A79A4D60DE6718E8E5B326E338AE533/10F2C57C1870517EAD822058C13907A38514E5EC24E869327D902E9D4B104E5F')
      .then(resp => resp.json())
      .then(result => {
        for (var i = 0; i < result.length; i++) {
          this.dataContent.push(result[i])
          this.dataContent[i].field_stoimost = {str: this.dataContent[i].field_stoimost, num: parseInt(this.dataContent[i].field_stoimost.replace(/\s{1,}/ig, ''))}
          this.dataContent[i].field_ploschad = {str: this.dataContent[i].field_ploschad, num: parseFloat(this.dataContent[i].field_ploschad.replace(/\s{1,}/ig, ''))}
          this.dataContent[i].field_ploschad_kukhni = {str: this.dataContent[i].field_ploschad_kukhni, num: parseFloat(this.dataContent[i].field_ploschad_kukhni.replace(/\s{1,}/ig, ''))}
          this.dataContent[i].field_ploschad_zhilaya = {str: this.dataContent[i].field_ploschad_zhilaya, num: parseFloat(this.dataContent[i].field_ploschad_zhilaya.replace(/\s{1,}/ig, ''))}
          this.dataContent[i].field_rayon = this.dataContent[i].field_rayon.toLowerCase()
          this.dataContent[i].field_fio = this.dataContent[i].field_fio .toLowerCase()
        }
      })
      
    },
    toAddNumber(){
      
      if (this.to === 0) {
        this.to = 10000000
      }
      
    },
    messages(a){
      
      if (a.id === 'from') {
        
        this.from = Number(a.val)
      } else if(a.id === 'to') {

        this.to = Number(a.val)
        
      } else if (a.id === 'val') {
       
        this.val = a.val.toLowerCase()
        
      } else {

        this.field = a.id

      }
    },
    componentVisible(){

      return 'sortBlock'

    },
    navigateVisible() {

      this.visible = !this.visible

    }
  }
}
</script>

<style lang="scss" scoped>

ul {
  margin: 0 !important;
  padding: 0 !important;
  list-style: none !important;
}

.vue-table {

$c:#3EA4EC;

font: {
        size:14px;
      }

& * {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

  border:1px solid red;
  margin: 0 auto;
  max-width: 1920px;
  width: 100%;

  font: {
    family:arial, sans-serif, helvetica;
  }

  &__head-body {

    width: 100%;
  }
  &__list {
      max-width: 100%;
      width: 100%;
      display: flex;
      justify-content: center;
      align-items: flex-start;

  }
  &__content {
    display: flex;
    justify-content: center;
    align-items: flex-start;
    flex-direction: column;
  }
  &__content-body {
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;

    /*border-right: 1px solid grey;

    &:last-child {
      border: none;
    }*/

    span {
      width: 100%;
      text-align: left;
    }
  }
  &__elem-head {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;

    width:100%;
    min-height: 50px;
    height: 100%;

    & > span {
      padding: 0 10px 0 10px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      color:white;
      background: $c;
      max-width: 136px;
      width: 100%;
      min-height: 50px;
      height: 100%;

      i {
        cursor: pointer;
      }
    }
  }
  &__content-column {
    display: flex;
    max-width: 100%;
    width: 100%;
    padding: 15px 0px;
    align-self: flex-start;

    span {
      padding: 0 10px 0 10px;
        max-width: 136px;
        width: 100%;
    }
  }

  & {
    .showPanel {
      display: block;
    }
    .hidePanel {
      display:none;
    }
  }
}

</style>