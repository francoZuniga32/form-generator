<template>
  <div class="form-check">
    Multiples Archivos
    <input
      class="form-check-input"
      type="checkbox"
      v-model="activo"
    />
    <label v-bind:for="input.id" class="form-check-label">input.label</label>
  </div>
</template>
<script>
export default{
    name: "input-file",
    data(){
        return{
            activo: false
        }
    }
}
</script>