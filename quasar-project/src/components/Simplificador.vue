<template>
     <div class="row q-ma-md" v-show="show">
           <div class="col-12 text-bold text-h4 q-mb-xl" style="color: rgb(165, 139, 139);">
               Simplificador de Fracciones: 
               <div class="row text-center q-mt-xl">
                    <div class="col-4">
                        <q-input mask="########" filled v-model="numerador" label="Numerador" />
                    </div>
                    <div class="col-4 text-bold text-h4 q-mb-md" style="color: rgb(165, 139, 139);">
                        /
                    </div>
                    <div class="col-4">
                        <q-input mask="########" filled v-model="denominador" label="Denominador" />
                    </div>
                </div>
           </div>
            
           <div class="col-12">
                <div class="row"> 
                    <div class="col-4"></div>
                    <div class="col-4">
                        <q-input filled label="Resultado" readonly v-model="resultado" />
                    </div>
                    <div class="col-4"> </div>
                </div>
            </div>

           <div class="col-12 text-center q-mt-xl">
                <div class="row"> 
                    <div class="col-4">
                        <q-btn color="positive" text-color="white" label="Calcular" @click="GetNumbers"></q-btn>
                    </div>
                    <div class="col-4">
                        
                    </div>
                    <div class="col-4">
                        <q-btn color="negative" text-color="white" label="Limpiar" @click="SetValues"></q-btn>
                    </div>
                </div>
            </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Simplificador',
    props:{
        show: Boolean
    },
    data(){
        return{
            numerador: null,
            denominador: null,
            resultado: null
        }
    },
    methods: {
        async GetSimplify(numerador, denominador){
          await axios.get(`https://localhost:7105/Fractions/GetFractionSimplify?numerador=` + numerador +`&denominador=`+ denominador +``)
            .then(done =>{
                this.resultado = done.data;
            })   
        },
        GetNumbers(){
            if(this.numerador != null && this.denominador != null){ 
                this.GetSimplify(this.numerador,this.denominador);
            }else{
                this.SendNotification("Debe ingresar parametros", "negative"); 
            }
        },
        SetValues(){
            this.numerador = null;
            this.denominador = null;
            this.resultado = null;
        },
        SendNotification(mensaje, color){
            this.$q.notify({
                message: mensaje,
                type: color,
                icon: "fas x-mark",
                position: "top",
                group: false,
            });
        },
    },
}
</script>