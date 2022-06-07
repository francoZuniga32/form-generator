<template>
    <div class="col-2">
        <button type="button" class="add" data-bs-toggle="modal" :data-bs-target="button">
            <span class="material-symbols-rounded">
                add
            </span>
        </button>

        <!-- Modal -->
        <div class="modal fade" v-bind:id="modal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="exampleModalLabel">
                            Cargar Input
                        </h5>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                        <div class="row">
                            <label for="Label">Nombre</label>
                            <input type="text" v-model="nombre" class="form-control">
                        </div>
                        <div class="row">
                            <label for="">Id</label>
                            <input type="text" v-model="id" class="form-control">
                        </div>
                        <div class="row">
                            <label for="">Label</label>
                            <input type="text" v-model="label" class="form-control">
                        </div>
                        <div class="row">
                            <label for="">Type</label>
                            <select name="" class="form-select" v-model="type">
                                <option value="text">Text</option>
                                <option value="number">Number</option>
                                <option value="password">Password</option>
                            </select>
                        </div>
                        <div class="row">
                            <label for="">Placeholder</label>
                            <input type="text" v-model="placeholder" class="form-control">
                        </div>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                        <button type="button" class="btn btn-primary" v-on:click="cargarInput">Cargar</button>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>
<script>
export default {
    name: "cargaInput",
    props: {
        indice: Number
    },
    mounted() {
        this.modal = `modal${this.indice}`;
        this.button = `#modal${this.indice}`;
    },
    data() {
        return {
            modal: "modal",
            button: "#modal",
            name: '',
            id: '',
            label: '',
            type: '',
            placeholder: ''
        }
    },
    methods: {
        cargarInput() {
            this.$emit('cargarInput', {
                id: this.indice,
                data: {
                    name: this.name,
                    id: this.id,
                    label: this.label,
                    type: this.type,
                    placeholder: this.placeholder
                }
            });
        }
    }
}
</script>
<style>

</style>