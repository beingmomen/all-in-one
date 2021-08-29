<template>
  <div>
    <section class="bmi">
        <Form @claculate="claculate" @saveData="saveData" :username="username" :unites="unites" :type="type" :conclusion="conclusion" :result="result" :personData="personData" :showElement="showElement" />
    </section>
    <DataStore @deleteCard="deleteCard" :dataStored="dataStored" :username="username" :type="type" :personData="personData" :result="result" :conclusion="conclusion" />
  </div>
</template>

<script>
import Form from './components/BMI/Form.vue'
import DataStore from './components/BMI/DataStore.vue'
export default {
    data() {
        return {
            showElement: false,
            personData: {
                weight: "",
                height: ""
            },
            result: "",
            conclusion: "",
            type: {
                name: "metric"
            },
            unites: {
                weightUnit: "kg",
                heightUnit: "cm"
            },
            username: {
                userInput: "",
                userPut: ""
            },
            dataStored: [],
        }
    },
    components: {
        Form,
        DataStore
    },
    methods: {
        claculate() {
            this.showElement = true

            if (this.type.name == "metric") {
                this.result = (this.personData.weight / (this.personData.height / 100) ** 2).toFixed(2)
            } else {
                this.unites.weightUnit = "lb"
                this.unites.heightUnit = "in"
                this.result = (703 * this.personData.weight / (this.personData.height ** 2)).toFixed(2)
            }

            if(this.result >= 16 && this.result <= 18.5) {
                this.conclusion = "Underweight"
            } else if (this.result > 18.5 && this.result <= 25) {
                this.conclusion = "Normal"
            } else if (this.result > 25 && this.result <= 30) {
                this.conclusion = "Overweight"
            } else {
                this.conclusion = ""
            }
        },
        saveData() {
            this.username.userPut = this.username.userInput
            this.dataStored.push
            ({
                name: this.username.userInput,
                system: this.type.name,
                weight: this.personData.weight,
                height: this.personData.height,
                result: this.result,
                conclusion: this.conclusion
            })
            this.showElement = false
            this.personData = {weight: "", height: ""}
        },
        deleteCard(i) {
            this.dataStored.splice(i, 1)
        }
    },
}
</script>

<style>
.bmi {
    margin: 50px auto;
    height: fit-content;
    padding-bottom: 30px;
    width: 400px;
    border: 1px solid #900C3F;
    border-radius: 4px;
    -webkit-border-radius: 4px;
    -moz-border-radius: 4px;
    -ms-border-radius: 4px;
    -o-border-radius: 4px;
    box-shadow: 0px 0px 10px #000, 0px 0px 10px #000;
    background-color: #581845;
}
</style>