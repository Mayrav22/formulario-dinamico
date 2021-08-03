<template>
  <div id="app">
    <b-container class="mt-5">
      <b-card>
        <b-card-title class="align-c-c text-primary"><b>Formulario de registro dinámico</b></b-card-title>
        <b-card-body>
            <Formulario :arrCampos="arrCampos"></Formulario>
            <b-row class="mt-4">
                <b-col cols="12" class="mb-3">
                    <b>Deseas agregar un nuevo campo?</b> &nbsp;&nbsp;
                    <b-button class="btn btn-success" size="sm" @click="agregarNuevoCampo=true">Agregar</b-button>
                </b-col>
                <b-col cols="12" v-if="agregarNuevoCampo">
                    <hr>
                    <b-row>
                        <b-col cols="12" sm="6" md="2">
                            <label for="nombreElemento">Indique nombre (id):</label>
                            <b-input size="sm" id="nombreElemento" v-model="datosNuevoCampo.nombreElemento" placeholder="Nombre..." />
                        </b-col>
                        <b-col cols="12" sm="6" md="2">
                            <label for="labelElemento">Indique label:</label>
                            <b-input size="sm" id="labelElemento" v-model="datosNuevoCampo.labelElemento" placeholder="Label..." />
                        </b-col>
                        <b-col cols="12" sm="6" md="3">
                            <label for="placeholderElemento">Indique placeholder:</label>
                            <b-input size="sm" id="placeholderElemento" v-model="datosNuevoCampo.placeholderElemento" placeholder="Placeholder..." />
                        </b-col>
                        <b-col cols="12" sm="6" md="2">
                            <label for="requiredElemento">Es requerido:</label>
                            <br>
                            <input type="checkbox" id="requiredElemento" v-model="datosNuevoCampo.requiredElemento" />
                        </b-col>
                        <b-col cols="12" sm="6" md="3">
                            <label for="elementoHTML">Que elemento desea agregar:</label>
                            <b-form-select  size="sm" id="elementoHTML" v-model="datosNuevoCampo.elementoHTML" :options="arrTiposElementosHTML"></b-form-select>
                        </b-col>
                        <b-col cols="12" sm="6" md="4" class="mt-3" v-if="datosNuevoCampo.elementoHTML == 'input'">
                            <label for="tipoInput">Indique que tipo de input:</label>
                            <b-form-select size="sm" id="tipoInput" v-model="datosNuevoCampo.tipoInput" :options="arrTiposInputs"></b-form-select>
                        </b-col>
                        <b-col cols="12" sm="6" md="4" class="mt-3" v-else-if="datosNuevoCampo.elementoHTML == 'select'">
                            <label for="opcionesSelect">Indique las options:</label>
                            <br>
                            <small class="text-secondary"><i>Por favor coloque (valor, texto) para las options del select y cada option separelas por enter</i></small>
                            <b-textarea size="sm" id="opcionesSelect" v-model="datosNuevoCampo.opcionesSelect" placeholder="Ej: value, texto"></b-textarea>
                        </b-col>
                        <b-col cols="12">
                            <b-row>
                                <b-col cols="6" class="mt-4 align-r-c">
                                    <b-button  class="btn btn-danger" size="sm" @click="agregarNuevoCampo=false, datosNuevoCampo={}">Cancelar</b-button>
                                </b-col>
                                <b-col cols="6" class="mt-4 align-l-c">
                                    <b-button  class="btn btn-success" size="sm" @click="FunAgregarNuevoCampo()">Guardar</b-button>
                                </b-col>
                            </b-row>
                        </b-col>
                    </b-row>
                    <hr>
                </b-col>
            </b-row>
        </b-card-body>
        <b-card-footer>
            <div class="align-c-c">
                <button class="btn btn-primary" @click="FuncEnviarForm">Enviar</button>
            </div>
        </b-card-footer>
      </b-card>
    </b-container>
  </div>
</template>

<script>
import Formulario from "./components/Formulario.vue";

export default {
    name: 'app',
    data () {
        return {
            agregarNuevoCampo: false,
            datosNuevoCampo: {
                nombreElemento: '',
                elementoHTML: undefined,
                tipoInput: undefined,
                opcionesSelect: '',
                labelElemento: '',
                placeholderElemento: ''
            },
            arrTiposElementosHTML: [
            { value: undefined, text: 'Por favor seleccione una opcion' },
            { value: 'input', text: 'Input' },
            { value: 'select', text: 'Select' },
            { value: 'textarea', text: 'Textarea' },
            ],
            arrTiposInputs: [
            { value: undefined, text: 'Por favor seleccione una opcion' },
            { value: 'checkbox', text: 'checkbox' },
            { value: 'color', text: 'color' },
            { value: 'date', text: 'date' },
            { value: 'datetime-local', text: 'datetime-local' },
            { value: 'email', text: 'email' },
            { value: 'file', text: 'file' },
            { value: 'month', text: 'month' },
            { value: 'number', text: 'number' },
            { value: 'password', text: 'password' },
            { value: 'radio', text: 'radio' },
            { value: 'range', text: 'range' },
            { value: 'search', text: 'search' },
            { value: 'tel', text: 'tel' },
            { value: 'text', text: 'text' },
            { value: 'time', text: 'time' },
            { value: 'url', text: 'url' },
            { value: 'week', text: 'week' },
            ],
            arrCampos: []
        }
    },
    components: {
        Formulario,
    },
    methods: {
        FunAgregarNuevoCampo() {
            this.arrCampos.push(this.datosNuevoCampo)
            this.agregarNuevoCampo = false
            this.datosNuevoCampo = {}
        },
        FuncEnviarForm() {
            alert('Finalizado')
            // Código para procesar el formulario
        }
    }
}

</script>

<style>
@import './assets/main.css';
</style>
