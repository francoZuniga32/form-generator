<template>
  <div>
    <div class="container">
      <div v-for="(nivel, i) in form" class="row nivel-padre" :key="i">
        <div class="row row-cols-2 nivel">
          <div class="col-10">
            <div class="row row-cols-3">
              <div v-for="(input, k) in nivel" class="col" :key="k">
                <label v-bind:for="input.id" class="form-label">{{ input.label }}</label>
                <input v-bind:type="input.type" class="form-control" v-bind:id="input.id"
                  v-bind:placeholder="input.placeholder">
              </div>
            </div>
          </div>
          <cargarInputVue :indice="i" v-on:cargarInput="cargarInput"></cargarInputVue>
        </div>
        <div class="row justify-content-center">
          <button class="add" v-on:click="addnivel(i)">
            <span class="material-symbols-rounded">
              add
            </span>
          </button>
          <button class="add" v-on:click="removenivel(i)">
            <span class="material-symbols-rounded">
              delete
            </span>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import cargarInputVue from './components/cargarInput.vue'
export default {
  name: 'App',
  components: {
    cargarInputVue
  },
  data() {
    return {
      form: [
        [
          {
            name: 'nombre',
            id: 'nombre',
            label: 'Nombre:',
            type: 'text',
            placeholder: ''
          },
          {
            name: 'apellido',
            id: 'apllido',
            label: 'Apellido:',
            type: 'text',
            placeholder: ''
          }
        ],
      ]
    }
  },
  methods: {
    cargarInput(data) {
      this.form[data.id].push(data.data);
    },
    addnivel(i) {
      console.log(i);
      if (this.form.length <= 1 || i == this.form.length - 1) {
        this.form.push([]);
      } else {
        if (i < this.form.length) {
          var inicio = this.form.slice(0, i + 1);
          var final = this.form.slice(i + 1);
          console.log(inicio, final);
          inicio.push([]);
          this.form = inicio.concat(final);
        }
      }
    },
    removenivel(i) {
      console.log(i);
      if (this.form.length <= 1) {
        this.form = [[]];
      } else if( i == this.form.length - 1){
        var antepenultimo = this.form.slice(0,i);
        this.form = antepenultimo;
      } {
        if (i < this.form.length - 1) {
          var inicio = this.form.slice(0, i);
          var final = this.form.slice(i+1);
          console.log(inicio, final);
          this.form = inicio.concat(final);
        }
      }
    }
  }
}
</script>
<style>
.nivel {
  display: flex;
  flex-direction: row;
  align-items: center;
}

.nivel-padre {
  display: flex;
  flex-direction: column;

}

.add {
  width: 40px;
  height: 40px;
  border: none;
  background-color: white;
  border-radius: 40px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.add:hover {
  background-color: darkgrey;
}
</style>