<template>
  <div class="row">
    <div class="col rounded-start bg-secondary " style="padding: 1%;">
      <select name="select" id="select" class="form-select">
        <option v-for="(data, i) in options" value="data.value" :key="i">
          {{ data.text }}
        </option>
      </select>
      <hr>
      <div class="">
        <div class="card d-flex" v-for="(data, k) in options" :key="k">
          <p>{{ data.text }}</p>
          <button class="btn btn-danger text-white" v-on:click="removenivel(k)">x</button>
        </div>
      </div>
    </div>
    <div class="col rounded-end bg-secondary" style="padding: 1%;">
      <input 
        type="text"
        class="form-control"
        v-model="value"
        placeholder="Value"
      />
      <br>
      <input
        type="text"
        class="form-control"
        v-model="text"
        placeholder="Text"
      />
      <br>
      <button v-on:click="add" class="btn btn-primary">Agregar Opcion</button>
    </div>
  </div>
</template>
<script>
export default {
  name: "SelectAdd",
  data() {
    return {
      options: [],
      value: null,
      text: null,
    };
  },
  methods: {
    add() {
      this.options.push({ value: this.value, text: this.text });
      this.value = null;
      this.text = null;
    },
    removenivel(i) {
      this.options.splice(i, 1);
      console.log(this.form);
    },
    getOptions() {
      return this.options;
    },
    refresh(){
      this.options = [];
      this.value = null;
      this.text = null;
    }
  },
};
</script>
