<template>
    <div class="row">
        <div class="row">
            <div class="col-sm">
                <label for="">Minimo</label>
                <input type="number" v-model="min" name="min" class="form-control" id=""/>
            </div>
            <div class="col-sm">
                <label for="">Maximo</label>
                <input type="number" v-model="max" name="max" class="form-control" id=""/>
            </div>
            <div class="col-sm">
                <label for="">Step</label>
                <input type="number" v-model="step" name="step" class="form-control" id=""/>
            </div>
        </div>
        
        <div class="row">
            <div class="col-sm">
                <input type="range" class="form-range" v-bind:min="min" v-bind:max="max" v-bind:step="step" id="range"/>
            </div>
        </div>
    </div>
</template>
<script>
export default{
    name: "range-selec",
    data(){
        return{
            max: 0,
            min: 0,
            step: 1,
        }
    }
}
</script>