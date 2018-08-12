<template>
    <div class="container">
        <h3>{{ title }}</h3>
        <div class="input-wrapper">
            <input type="text" class="amount-field" :value="sliderValue">
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
            sliderValue: 0
        }
    },
    methods: {
        sliderChange() {                
            this.$emit("sliderChange", this.sliderValue)
        }
    }
}
</script>

<style src="./Slider.css"></style>
