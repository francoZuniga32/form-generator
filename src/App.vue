<template>
  <div>
    <navbar></navbar>
    <div class="container">
      <div v-if="form.length > 0" class="container" id="formulario">
        <div v-for="(nivel, i) in form" class="row nivel-padre" :key="i">
          <div class="row row-cols-2 nivel">
            <div class="col-10">
              <div v-bind:class="css(i)">
                <div v-for="(input, k) in nivel.inputs" class="col" :key="k">
                  <div v-if="input.type == 'select'">
                    <label v-bind:for="input.id">{{ input.label }}</label>
                    <select
                      class="form-select"
                      v-bind:name="input.name"
                      v-bind:id="input.id"
                    >
                      <option
                        v-for="(option, j) in input.options"
                        :key="j"
                        v-bind:value="option.value"
                      >
                        {{ option.text }}
                      </option>
                    </select>
                    
                  </div>
                  <div v-else-if="input.type == 'range'">
                    <label v-bind:for="input.id">{{ input.label }}</label>
                    <input
                      type="range"
                      class="form-range"
                      v-bind:min="input.min"
                      v-bind:max="input.max"
                      v-bind:step="input.step"
                      id="range"
                    />
                  </div>
                  <div v-else-if="input.type == 'checkbox'">
                    <div class="form-check">
                      sdfsdfsdf
                      <input
                        class="form-check-input"
                        type="checkbox"
                        v-bind:id="id"
                        v-bind:name="name"
                      />
                      <label v-bind:for="input.id" class="form-check-label"
                        >input.label</label
                      >
                    </div>
                  </div>
                  <div v-else-if="input.type == 'switch'">
                    <div class="form-check form-switch">
                      <input
                        class="form-check-input"
                        type="checkbox"
                        v-bind:id="input.id"
                        v-bind:name="input.name"
                      />
                      <label class="form-check-label" v-bind:for="input.id">{{
                        input.label
                      }}</label>
                    </div>
                  </div>
                  <div v-else-if="input.type == 'file'">
                    <div>
                      <label v-bind:for="input.id" class="form-label">{{
                        input.label
                      }}</label>
                      <input
                        class="form-control"
                        type="file"
                        v-bind:id="id"
                        v-bind:name="input.name"
                      />
                    </div>
                  </div>
                  <div v-else-if="input.type == 'color'">
                    <div>
                      <label v-bind:for="input.id" class="form-label">{{
                        input.label
                      }}</label>
                      <input
                        type="color"
                        class="form-control form-control-color"
                        v-bind:id="id"
                        value="#000"
                        title="Seleccione un Color"
                        v-bind:name="name"
                      />
                    </div>
                  </div>
                  <div v-else-if="input.type == 'date'">
                    <label v-bind:for="input.id">{{input.label}}</label>
                    <input class="form-control" type="date" v-bind:name="input.name" v-bind:id="input.date">
                  </div>
                  <div v-else-if="input.type == 'time'">
                    <label v-bind:for="input.id">{{input.label}}</label>
                    <input class="form-control" type="time" v-bind:name="input.name" v-bind:id="input.date">
                  </div>
                  <div v-else>
                    <label v-bind:for="input.id" class="form-label">{{
                      input.label
                    }}</label>
                    <input
                      v-bind:type="input.type"
                      class="form-control"
                      v-bind:id="input.id"
                      v-bind:placeholder="input.placeholder"
                    />
                  </div>
                  <button class="btn btn-ligth" v-on:click="removeInput(i, k)">
                    <span class="material-symbols-rounded"> delete </span>
                  </button>
                </div>
              </div>
            </div>
            <cargarInputVue
              :indice="i"
              v-on:cargarInput="cargarInput"
            ></cargarInputVue>
            <div class="col-1">
              <div>
                Brackpoints
              </div>
              <div class="row">
                sm 
                <input type="number" class="form-control" v-model="nivel.colssm" min="1" max="12" v-on:change="loadhtml"> 
              </div>
              <div class="row d-flex">
                md 
                <input type="number" class="form-control" v-model="nivel.colsmd" min="1" max="12" v-on:change="loadhtml"> 
              </div>
              <div class="row">
                lg 
                <input type="number" class="form-control" v-model="nivel.colslg"  min="1" max="12" v-on:change="loadhtml"> 
              </div>
            </div>
          </div>
          <div class="row justify-content-center">
            <button class="add" v-on:click="addnivel(i)">
              <span class="material-symbols-outlined"> add </span>
            </button>
            <button class="add" v-on:click="removenivel(i)">
              <span class="material-symbols-rounded"> delete </span>
            </button>
          </div>
          <hr />
        </div>
      </div>
      <div v-else>
        <div class="row justify-content-center">
          <button class="add" v-on:click="addnivel(i)">
            <span class="material-symbols-outlined"> add </span>
          </button>
          <button class="add" v-on:click="removenivel(i)">
            <span class="material-symbols-rounded"> delete </span>
          </button>
        </div>
      </div>
      <h1>Codigo</h1>
      <hr />
      <button class="add" v-on:click="clipboard()">
        <span class="material-symbols-rounded"> content_paste </span>
      </button>
      <textarea class="form-control" rows="15" v-model="html"> </textarea>
    </div>
  </div>
</template>

<script>
import cargarInputVue from "./components/cargarInput.vue";
import navbar from "./components/navbar.vue";

export default {
  name: "App",
  components: {
    cargarInputVue,
    navbar,
  },
  data() {
    return {
      form: [
        {
          colssm:1,
          colsmd: 2,
          colslg: 3,
          inputs:[
            {
              name: "nombre",
              id: "nombre",
              label: "Nombre:",
              type: "text",
              placeholder: "",
            },
            {
              name: "apellido",
              id: "apllido",
              label: "Apellido:",
              type: "text",
              placeholder: "",
            },
          ],
        }
        
      ],
      html: "",
    };
  },
  
  mounted() {
    this.loadhtml();
  },
  methods: {
    css(cols){
      return `row row-cols-sm-${this.form[cols].colssm} row-cols-md-${this.form[cols].colsmd}  row-cols-lg-${this.form[cols].colslg}  d-flex align-items-end`
    },
    cargarInput(data) {
      this.form[data.id].inputs.push(data.data);
      console.log(data);
      this.loadhtml();
    },
    addnivel(i) {
      console.log(i);
      if (this.form.length <= 1 || i == this.form.length - 1) {
        this.form.push({
          colssm:1,
          colsmd: 2,
          colslg: 3,
          inputs: []
        });
      } else {
        if (i < this.form.length) {
          var inicio = this.form.slice(0, i + 1);
          var final = this.form.slice(i + 1);
          console.log(inicio, final);
          inicio.push({
            colssm:1,
            colsmd: 2,
            colslg: 3,
            inputs:[]
          });
          this.form = inicio.concat(final);
        }
      }
      this.loadhtml();
    },
    removenivel(i) {
      this.form.splice(i, 1);
      console.log(this.form);
    },
    removeInput(idNivel, id){
      this.form[idNivel].inputs.splice(id, 1);
    },  
    async loadhtml() {
      var html = `<form class="container" method="" action="">\n`;
      for (let j = 0; j < this.form.length; j++) {
        var nivel = this.form[j].inputs;
        var nivelHtml = `\t<div class="row row-cols-sm-${this.form[j].colssm} row-cols-md-${this.form[j].colsmd} row-cols-lg-${this.form[j].colslg} ">\n`;

        for (let i = 0; i < nivel.length; i++) {
          console.log(nivel[i]);
          var { name, id, label, type, placeholder, min, max, step, options } =
            nivel[i];
          nivelHtml += `\t\t<div class="col">\n`;
          switch (type) {
            case "text":
              nivelHtml += `\t\t\t${await this.inputText(
                label,
                name,
                id,
                placeholder
              )}\n`;
              break;
            case "number":
              nivelHtml += `\t\t\t${await this.inputNumber(
                max,
                min,
                label,
                name,
                id,
                placeholder
              )}\n`;
              break;
            case "password":
              nivelHtml += `\t\t\t${await this.inputPassword(
                label,
                name,
                id,
                placeholder
              )}\n`;
              break;
            case "range":
              nivelHtml += `\t\t\t${await this.inputRange(
                min,
                max,
                step,
                label,
                name,
                id
              )}\n`;
              break;
            case "select":
              nivelHtml += `\t\t\t${await this.inputSelect(
                options,
                label,
                name,
                id
              )}\n`;
              break;
            case "checkbox":
              nivelHtml += `\t\t\t\t${await this.inputCheckbox(label, name, id)}`;
              break;
            case "switch":
              nivelHtml += `\t\t\t${await this.inputSwich(label, name, id)}`;
              break;
            case "file":
              nivelHtml += `\t\t\t${await this.inputFile(label, name, id)}`;
              break;
            case "color":
              nivelHtml += `\t\t\t${await this.inputColor(label, name, id)}`;
              break;
            case "date":
              nivelHtml += `\t\t\t${await this.inputDate(label, name, id)}`;
              break;
            case "time": 
              nivelHtml += `\t\t\t${await this.inputTime(label, name, id)}`;
              break;
          }
          nivelHtml += `\t\t</div>\n`;
        }
        nivelHtml += `\t</div>\n`;
        html += nivelHtml;
      }
      html += `</form>`;
      this.html = html;
    },

    clipboard() {
      /* Copy the text inside the text field */
      navigator.clipboard.writeText(this.html);
    },

    async inputText(label, name, id, placeholder) {
      return `
        <label for="${id}" class="form-label">${label}</label>
        <input type="text" class="form-control" id="${id}" name="${name}" placeholder="${placeholder}"/>
      `;
    },
    async inputPassword(label, name, id, placeholder) {
      return `
        <label for="${id}" class="form-label">${label}</label>
        <input type="password" class="form-control" id="${id}" name="${name}" placeholder="${placeholder}"/>
      `;
    },
    async inputNumber(max, min, label, name, id, placeholder) {
      return `
        <label for="${id}" class="form-label">${label}</label>
        <input type="number" max="${min}" max="${max}" class="form-control" id="${id}" name="${name}" placeholder="${placeholder}"/>
      `;
    },
    async inputCheckbox(label, name, id) {
      return `
      <div class="form-check">
        <input class="form-check-input" type="checkbox" id="${id}" name="${name}"/>
        <label for="${id}" class="form-check-label">${label}</label>
      </div>
      `;
    },
    async inputDate(label, name, id){
      return `
        <label for="${id}" class="form-check-label">${label}</label>
        <input class="form-control" type="date" id="${id}" name="${name}"/>
      `;
    },
    async inputTime(label, name, id){
      return `
        <label for="${id}" class="form-check-label">${label}</label>
        <input class="form-control" type="time" id="${id}" name="${name}"/>

      `;
    },
    async inputRange(min, max, step, label, name, id) {
      return `
        <label for="${id}" class="form-label">${label}</label>
        <input type="range" class="form-range" name="${name}" id="${id}" min="${min}" max="${max}" step="${step}">
      `;
    },
    async inputSelect(options, label, name, id) {
      var retorno = `<label for="${id}" class="form-label">${label}</label>\n
        <select class="form-control" id="${id}" name="${name}">
      `;
      console.log(options);
      for (let i = 0; i < options.length; i++) {
        const option = options[i];
        retorno += `<option value="${option.value}" >${option.text}</option>\n`;
      }

      retorno += `</select>`;
      return retorno;
    },
    async inputSwich(label, name, id) {
      return `
      <div class="form-check form-switch">
        <input
          class="form-check-input"
          type="checkbox"
          id="${id}"
          name="${name}"
        />
        <label
          class="form-check-label"
          for="${id}"
          >${label}</label
        >
      </div>
      `;
    },
    async inputFile(label, name, id) {
      return `
        <div>
          <label for="${id}" class="form-label">${label}</label>
          <input class="form-control" type="file" id="${id}" name="${name}">
        </div>
      `;
    },
    async inputColor(label, name, id) {
      return `
        <div>
          <label for="${id}" class="form-label">${label}</label>
          <input type="color" class="form-control form-control-color" id="${id}" value="#000" title="Seleccione un Color" name="${name}">
        </div>
      `;
    },
  },
};
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

button {
  align-items: center;
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
