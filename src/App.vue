<template>
    <div id="app">
        <h1>Calculate your desired loan</h1>
        <div class="wrapper">
            <Slider 
              title="How much would you like to loan?" 
              :min="25000"               
              :max="100000"
              minDisplay="S$ 25,000"
              maxDisplay="S$ 100,000"/>

            <Slider
              title="What is your preferred tenor?" 
              :min="1"               
              :max="24"
              minDisplay="1 month"
              maxDisplay="24 months"/>
            
            <button name="calculate"> Calculate </button>
        </div>
    </div>
</template>

<script>
import Slider from './components/slider/Slider.vue'

export default {
    name: 'app',
    components: {
        Slider
    }
}
</script>

<style src="./Style.css"></style>
