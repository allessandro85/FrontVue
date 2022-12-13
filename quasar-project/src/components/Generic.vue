<template>
    <div class="row q-ma-md">
        <q-card class="q-pa-md">
            <div class="col-12">
                <q-card-section class="bg-teal text-white">
                    <div class="text-h4 text-center"> Desafío Técnico </div>
                    <div class="text-h3 text-center"> Alejandro Piñero </div>
                    <div class="text-h5 q-mt-md" >{{ title }}</div>
                </q-card-section>
            </div>
            <div class="col-12 text-bold text-h4 q-mb-xl" style="color: rgb(165, 139, 139);">
              <div class="row text-center q-mt-xl" v-if="fieldTypeNumber">
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
               <div class="row text-center q-mt-xl" v-else>
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

           <div class="row text-center">
            <div class="col-12 text-h6 q-mb-md q-mt-md">
                {{texto}}
            </div>
           </div>

          <div class="col-12 text-center q-mt-xl">
               <div class="row"> 
                   <div class="col-4">
                       <q-btn color="positive" text-color="white" label="Calcular" @click="GetData"></q-btn>
                   </div>
                   <div class="col-4">
                       
                   </div>
                   <div class="col-4">
                       <q-btn color="negative" text-color="white" label="Limpiar" @click="SetValues"></q-btn>
                   </div>
               </div>
           </div>
        </q-card>
   </div>
</template>

<script>
import axios from 'axios'

export default {
   name: 'Generic',
   props:{
       title: String,
       fieldTypeNumber: Boolean,
       texto: String,
   },
   data(){
       return{
           numerador: null,
           denominador: null,
           resultado: null,
           nombre: null,
           apellido: null,
           error: true,
           url: null
       }
   },
   methods: {
        async GetDataApi(type){
            this.error = false;
            if(type == "Validation"){
                this.url = "https://localhost:7105/Validation/GetValidationName?name=" + this.nombre +`&surname=`+ this.apellido +``;
            }else{
                this.url = "https://localhost:7105/Fractions/GetFractionSimplify?numerador="+ this.numerador +`&denominador=`+ this.denominador +``;
            }

            await axios.get(this.url)
            .then(done =>{
                this.resultado = done.data;
            })
        },
       GetData(){ debugger;
        if(this.fieldTypeNumber){
            if(this.numerador != null && this.denominador != null){
                this.GetDataApi("Fractions");
            }
        }else{
            if((this.nombre != null && this.apellido != null) && (this.nombre != ' ' && this.apellido != ' ')){
                this.GetDataApi("Validation");
            }
        }

        if(this.error){
            this.SendNotification("Debe ingresar parametros", "negative"); 
        }

       },
       SetValues(){
           this.numerador = null;
           this.denominador = null;
           this.nombre = null;
           this.apellido = null;
           this.resultado = null;
       },
       SendNotification(mensaje, color){
           this.$q.notify({
               message: mensaje,
               type: color,
               position: "top",
               group: false,
           });
       },
   },
}
</script>