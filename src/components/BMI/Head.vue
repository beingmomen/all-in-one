<template>
    <div>
        <div id="heading" class="heading">
            <h2 class="heading-title">System</h2>
            <input @change="chooseMetric" v-model="type.name" id="metric" class="metric-input" type="radio" name="units" value="metric" />
            <label for="metric" class="metric-name">Metric</label>
            <input @change="chooseImperial" v-model="type.name" id="imperial" class="imperial-input" type="radio" name="units" value="imperial" />
            <label for="imperial" class="imperial-name">Imperial</label>
        </div>
        <hr>
    </div>
</template> 
<script>
export default {
    props: ["type", "unites"],
    methods: {
        chooseMetric() {
            if (this.type.name = "metric") {
                this.unites.heightUnit = "cm"
                this.unites.weightUnit = "kg"
            }
        },
        chooseImperial() {
            if (this.type.name = "imperial") {
                this.unites.heightUnit = "in"
                this.unites.weightUnit = "lb"
            }
        }
    }
}
</script>

<style>
.heading {
    display: flex;
    justify-content: space-between;
}

.heading-title {
    color: #FF5733;
    margin-top: 10px;
    margin-left: 15px;
    width: fit-content;
}

.heading input {
    margin-top: 27px;
    margin-right: -25px;
}

label {
    color: #DAF7A6;
    font-size: 20px;
    margin-top: 18px;
    margin-right: 15px;
}

.metric-name {
    margin-right: 10px;
}

hr {
    background-color: #900C3F !important;
    width: 90%;
    height: 1px !important;
    opacity: 1 !important;
    margin: 1rem auto !important;
}
</style>