<template>
    <div class="row q-ma-md"  v-show="show">
        <div class="col-12 text-bold text-h4 q-mb-xl" style="color: rgb(165, 139, 139);">
            Validador: 
            <div class="row text-center q-mt-xl">
                <div class="col-4">
                    <q-input filled v-model="nombre" label="Ingrese nombre" />
                </div>
                <div class="col-4 text-bold text-h4 q-mb-md" style="color: rgb(165, 139, 139);">
                </div>
                <div class="col-4">
                    <q-input filled v-model="apellido" label="Ingrese apellido" />
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
                    <q-btn color="positive" text-color="white" label="Calcular" @click="GetName"></q-btn>
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
   name: 'ValidadorNombre',
   props:{
        show: Boolean
   },
   data(){
        return{
            nombre: null,
            apellido: null,
            resultado: null
        }
    },
    methods: {
        async GetSimplify(){
          await axios.get(`https://localhost:7105/Validation/GetValidationName?name=` + this.nombre +`&surname=`+ this.apellido +``)
            .then(done =>{
                this.resultado = done.data;
            })   
        },
        GetName(){
            if( (this.nombre != null && this.apellido != null) && (this.nombre != ' ' && this.apellido != ' ') ){
                this.GetSimplify();
            }else{
                this.SendNotification("Debe ingresar parametros", "negative"); 
            }
        },
        SetValues(){
            this.nombre = null;
            this.apellido = null;
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