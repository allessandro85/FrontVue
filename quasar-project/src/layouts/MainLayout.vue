<template>
  <q-layout view="lHh Lpr lFf">
    <div class="row">
      <div class="col-2"></div>
      <div class="col-8">
        <Generic ref="generic" :texto="texto" :title="titulo" :fieldTypeNumber="fieldTypeNumber"></Generic>
        <div class="row q-mt-md">
          <q-btn class="col-6" color="primary" label="Simplificador" size="md" @click="ShowSimplificador"/>
          <q-btn class="col-6" color="positive" label="Validador" size="md" @click="ShowValidacion"/>
        </div>
      </div>
    </div>
  </q-layout>
</template>

<script>
import Generic from 'components/Generic.vue'
import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'MainLayout',
  components: {
    Generic
  },
  mounted(){
    this.ShowSimplificador();
  },
  data () {
    return {
      texto: null,
      titulo: null,
      fieldTypeNumber: null
    }
  },
  methods:{
    ShowSimplificador(){
      this.titulo = "Simplificacion de Fracciones";
      this.fieldTypeNumber = true;
      this.SetValues();
      this.texto = "Crear una función que devuelva una versión simplificada de una fracció Ejemplos a) Simplificar(4/6) = 2/3 b) Simplificar(10/11) = 10/11 c) Simplificar(100/400) = 10/4 Notas: una fracción simplificada no tiene divisores comunes mínimos (excepto 1) entre el numerador y el  denominador. Por ejemplo, 4/6 no está simplificada, ya que tanto 4 y 6 comparten 2 como factor Si una fracción puede ser transformada en enteró, también debe tenerse en cuenta";
    },
    ShowValidacion(){
      this.titulo = "Validacion de Nombre";
      this.fieldTypeNumber = false;
      this.SetValues();
      this.texto = "Tener en cuenta las siguientes definiciones a) El término ingresado pueden ser iniciales o palabras completas b) Una inicial es solo un carácter más un punto c) Una palabra se comprende de 2 o más caracteres, sin punto.  a) Tanto las iniciales como las palabras completas deben estar capitalizadas (la primera letra en  mayúsculas) b) Las iniciales deben terminar en punto (.) c) Solo habrán 2 o 3 términos en el ingreso. Es decir, o dos nombres y un apellido o solo un nombre y  un apellido d) Si se ingresan dos nombres y un apellido, los dos primeros pueden ser iniciales, o solo el segundo. Nunca puede ser una inicial el primer nombre y no el segundo e) El apellido siempre debe ser una palabra completa f) LA tarea consiste en escribir una función que, siguiendo las reglas anteriores, devuelva si un nombre es válido (true) o no (false).";
    },
    SetValues(){
      if(this.$refs && this.$refs.generic){
        this.$refs.generic.SetValues();
      }
    }
  }
})
</script>
