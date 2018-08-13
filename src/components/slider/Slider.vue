<template>
    <div class="container">
        <h3>{{ title }}</h3>
        <div class="input-wrapper">
            <input type="text" v-bind:class="{ valid : valid, invalid : invalid }" class="amount-field" :value="sliderValue | amount" v-on:change="inputChange">
            <div class="range-slider-container">
                <input v-model="sliderValue" type="range" :min="min" :max="max" class="slider" @change="sliderChange" />
                <div class="amount-range-container">
                    <div id="min">{{ minDisplay }}</div>
                    <div id="max">{{ maxDisplay }}</div>
                </div>
            </div> 
        </div> 
    </div>    
</template>

<script>
export default {
    name: "Slider",
    props: {
        title: String,
        name: String,
        min: Number,
        max: Number,
        minDisplay: String,
        maxDisplay: String
    },
    data: function() {
        return {
            sliderValue: this.$props.min,
            valid: true,
            invalid: false
        }
    },
    methods: {
        sliderChange() {                
            this.$emit("sliderChange", this.sliderValue)
            let value = this.sliderValue
            let max = this.$props.max
            let min = this.$props.min
            if (value < min || value > max) {
                this.$data.valid = false
                this.$data.invalid = true
            } else {
                this.$data.valid = true
                this.$data.invalid = false
            }
        },
        inputChange($event) {
            let value = $event.target.value
            let max = this.$props.max
            let min = this.$props.min
            if (value < min || value > max) {
                this.$data.valid = false
                this.$data.invalid = true
            } else {
                this.$data.valid = true
                this.$data.invalid = false
            }
            this.sliderValue = $event.target.value;
        }
    },
    filters: {
        amount : function(value) {
            if (!value) return value
            value = parseFloat(value).toFixed(2)
            return Number(value).toLocaleString('en')
        }
    }
}
</script>

<style src="./Slider.css"></style>
