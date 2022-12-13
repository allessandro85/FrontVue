<template>
    <div class="row q-ma-md" v-show="show">
       <div class="row text-center">
          <div class="col-12 text-h6 q-mb-xl">
              {{texto}}
          </div>
      </div>
   </div>
</template>

<script>
export default {
    name: 'Reglas',
    props:{
        texto: String,
        show: Boolean
    }
}
</script>