<template>
  <div class="col-2">
    <button
      type="button"
      class="add"
      data-bs-toggle="modal"
      :data-bs-target="button"
    >
      <span class="material-symbols-rounded"> add </span>
    </button>

    <!-- Modal -->
    <div
      class="modal fade"
      v-bind:id="modal"
      tabindex="-1"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-xl">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Cargar Input</h5>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <div class="row">
              <div class="col-sm">
                <label for="Label">Nombre</label>
                <input type="text" v-model="name" class="form-control" />
              </div>
              <div class="col-sm">
                <label for="">Id</label>
                <input type="text" v-model="id" class="form-control" />
              </div>
            </div>
            <div class="row">
              <div class="col-sm">
                <label for="">Label</label>
                <input type="text" v-model="label" class="form-control" />
              </div>
              <div class="col-sm">
                <label for="">Type</label>
                <select
                  name=""
                  class="form-select"
                  v-on:change="selected"
                  v-model="type"
                >
                  <option value="text">Text</option>
                  <option value="number">Number</option>
                  <option value="password">Password</option>
                  <option value="select">Select</option>
                  <option value="range">Range</option>
                  <option value="checkbox">Checkbox</option>
                  <option value="switch">Switch</option>
                  <option value="file">Archivo</option>
                  <option value="color">Color</option>
                </select>
              </div>
            </div>
            <div class="row">
              <div class="col-sm">
                <label for="">Placeholder</label>
                <input type="text" v-model="placeholder" class="form-control" />
              </div>
            </div>
            <hr />
            <div class="row">
              <selectAdd v-if="display_options.select" ref="selectAdd" />
            </div>
            <div v-if="display_options.range" class="row">
              <range ref="rangeAdd" />
            </div>
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-bs-dismiss="modal"
            >
              Close
            </button>
            <button
              type="button"
              class="btn btn-primary"
              v-on:click="cargarInput"
            >
              Cargar
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import selectAdd from "./select.vue";
import range from "../components/range.vue";

export default {
  name: "cargaInput",
  components: {
    selectAdd,
    range,
  },
  props: {
    indice: Number,
  },
  mounted() {
    this.modal = `modal${this.indice}`;
    this.button = `#modal${this.indice}`;
  },
  data() {
    return {
      modal: "modal",
      button: "#modal",
      name: "",
      id: "",
      label: "",
      type: "",
      placeholder: "",
      options: {},
      display_options: {
        select: false,
        number: false,
        range: false,
      },
    };
  },
  methods: {
    selected() {
      Object.keys(this.display_options).forEach((key) => {
        this.display_options[key] = false;
      });
      switch (this.type) {
        case "select":
          this.display_options.select = true;
          break;
        case "range":
          this.display_options.range = true;
          break;
        case "number":
          this.display_options.number = true;
          break;
      }
    },
    cargarInput() {
      var data = {
        name: this.name,
        id: this.id,
        label: this.label,
        type: this.type,
        placeholder: this.placeholder
      };
      switch (this.type) {
        case "select":
          data.options = [...this.$refs.selectAdd.options];
          break;
        case "range":
          data.max = this.$refs.rangeAdd.max;
          data.min = this.$refs.rangeAdd.min;
          data.step = this.$refs.rangeAdd.step;
          break;
        
      }
      this.$emit("cargarInput", {
        id: this.indice,
        data,
      });
      this.name = "";
      this.id = "";
      this.label = "";
      this.type = "";
      this.placeholder = "";
    },
  },
};
</script>
<style></style>
