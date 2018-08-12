<template>
    <div id="app">
        <h1>Calculate your desired loan</h1>
        <div class="wrapper">
            <Slider 
                title="How much would you like to loan?" 
                ref="amountSlider"
                :min="25000"               
                :max="100000"
                minDisplay="S$ 25,000"
                maxDisplay="S$ 100,000"/>

            <Slider
                title="What is your preferred tenor?" 
                ref="tenorSlider"
                :min="1"               
                :max="24"
                minDisplay="1 month"
                maxDisplay="24 months"/>

            <button name="calculate" v-on:click="getRepayment"> Calculate </button>       
        </div>          
        <div class="breaker">&nbsp;</div>

        <h2>Computed Repayment</h2>
        <div class="wrapper">
            <div class="computed-repayment">
                <ResultItem title="Monthly" value="S$4,500" />
                <ResultItem title="Interest Rate" value="1.2 %" />
                <ResultItem title="Interest Amount" value="S$101, 200" />
                <ResultItem title="Tenor" value="1 year, 8 months" />                
            </div>            
        </div>
    </div>
</template>

<script>
//imports
import Slider from './components/slider/Slider.vue'
import ResultItem from './components/ResultItem.vue'

export default {
    name: 'app',
    components: {
        Slider,
        ResultItem
    },
    methods : {
        getRepayment: function() {
            let loanAmount = this.$refs.amountSlider.sliderValue;
            let tenor = this.$refs.tenorSlider.sliderValue
            console.log(`Loan amount ${loanAmount}, tenor: ${tenor}`)
        }
    }
}
</script>

<style src="./Style.css"></style>
