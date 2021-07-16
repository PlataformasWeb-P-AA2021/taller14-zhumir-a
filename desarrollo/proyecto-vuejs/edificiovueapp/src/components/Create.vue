<template>
<div class="pt-5">
    <form @submit.prevent="create" method="post">
        <div class="form-group">
            <label for="propietario">Nombre del propietario</label>
            <input type="text" class="form-control" id="propietario" v-model="departamento.propietario" v-validate="'required'" name="propietario" placeholder="Ingrese nombre del propietario" :class="{'is-invalid': errors.has('departamento.propietario') && submitted}">
            <div class="invalid-feedback">
                Please provide a valid name.
            </div>
        </div>
        <div class="form-group">
            <label for="costo">Costo del departamento</label>
            <input type="text" class="form-control" id="costo" v-model="departamento.costo" v-validate="'required'" name="costo" placeholder="Ingrese el costo" :class="{'is-invalid': errors.has('departamento.costo') && submitted}">
            <div class="invalid-feedback">
                Please provide a valid name.
            </div>
        </div>
        <div class="form-group">
            <label for="numCuartos">Número de Cuartos</label>
            <input type="text" class="form-control" id="num_cuartos" v-model="departamento.num_cuartos" v-validate="'required'" name="num_cuartos" placeholder="Ingrese el número de cuartos" :class="{'is-invalid': errors.has('departamento.num_cuartos') && submitted}">
            <div class="invalid-feedback">
                Please provide a valid name.
            </div>
        </div>
        <div class="form-group">
            <label for="edificio">Edificio</label>
            <select class="form-control" v-model="departamento.edificio">
                <option v-for="e in edificiosList" :key="e.url" :value="e.url">{{ e.nombre }}</option>
            </select>
        </div>
        <br>
        <div>
            <br>
            <button type="submit" class="btn btn-primary">Crear</button>
        </div>
    </form>
</div>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {
            departamento: {
                propietario: '',
                costo: '',
                numCuartos: '',
                edifcio: '',
            },
            edificiosList: [],
            submitted: false
        }
    },
    mounted() {
        this.getEdificiosList()
    },
    methods: {
        getEdificiosList() {
            axios
                .get('http://127.0.0.1:8090/api/edificios/')
                .then(response => {
                    this.edificiosList = response.data
                })
                .catch(error => {
                    console.log(error)
                })
        },
        create: function (e) {
            this.$validator.validate().then(result => {
                this.submitted = true;
                if (!result) {
                    return;
                }
                
                axios.post('http://127.0.0.1:8090/api/departamentos/',
                        this.departamento
                    )
                    .then(response => {
                        this.$router.push('/');
                    })
            });
        }
    },
}
</script>