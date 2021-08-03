<template>
  <div>
  <form>
    <b-row>
        <b-col cols="3">
            <label for="nombres">Nombres:</label>
            <b-input id="nombres" placeholder="Nombres..." />
        </b-col>
        <b-col cols="3">
            <label for="apellidos">Apellidos:</label>
            <b-input id="apellidos" placeholder="Apellidos..." />
        </b-col>
        <b-col cols="3">
            <label for="correo">Correo:</label>
            <b-input id="correo" placeholder="Correo..." />
        </b-col>
        <b-col cols="3">
            <label for="password">Password:</label>
            <b-input id="password" placeholder="Password..." />
        </b-col>
        <b-col cols="3" class="mt-3" v-for="(campo, i) in arrCampos" :key="i">
            <label :for="campo.nombreElemento" class="text-capitalize"> <b class="text-danger" v-if="campo.requiredElemento">*</b> {{campo.labelElemento}} :</label>
            <!--INPUT-->
            <input class="form-control" v-if="campo.elementoHTML == 'input'" :id="campo.nombreElemento" :type="campo.tipoInput" :placeholder="campo.placeholderElemento" :required="campo.requiredElemento"/>
            <!--SELECT-->
            <b-select v-else-if="campo.elementoHTML === 'select'" :name="campo.nombreElemento" :required="campo.requiredElemento">
                <option v-for="(opcion, n) in FuncOrganizarOptions(campo.opcionesSelect)" :key="n" :value="opcion.valor">
                    {{opcion.texto}}
                </option>
            </b-select>
            <!--TEXTAREA-->
            <b-textarea v-else-if="campo.elementoHTML === 'textarea'" :id="campo.nombreElemento" :placeholder="campo.placeholderElemento" :required="campo.requiredElemento"/>
        </b-col>
    </b-row>
  </form>
  </div>
</template>

<script>
export default {
    name: 'FormControls',
    data () {
        return {
        arrTiposInputs: [
            'checkbox',
            'color',
            'date',
            'datetime-local',
            'email',
            'file',
            'month',
            'number',
            'password',
            'radio',
            'range',
            'search',
            'tel',
            'text',
            'time',
            'url',
            'week',
        ]
        }
    },
    props: ['arrCampos'],
    methods: {
        FuncOrganizarOptions(string) {
            let arrFinal = []
            let arr1 = string.split('\n')
            arr1.forEach(string2 => {
                let arr2 = string2.split(',')
                let obj = {valor: arr2[0], texto: arr2[1]}
                arrFinal.push(obj)
            });
            return arrFinal
        }
    }
}
</script>