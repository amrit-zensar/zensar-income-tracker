<template>
  <!-- <h1>Hello Vue</h1> -->
  <Header :totalIncome="state.totalIncome" />
  <Form :state="state" @add-income="AddIncome" />
  <IncomeList :state="state" />
</template>

<script>
import { reactive, computed } from 'vue';
import Header from './components/Header.vue';
import Form from './components/Form.vue';
import IncomeList from './components/IncomeList.vue';


export default {
  name: 'App',
  components: {
    Header,
    Form,
    IncomeList,
  },
  setup() {
    const state = reactive ({
      income: [],
      totalIncome: computed(() => {
        let temp = 0;
        if (state.income.length > 0) {
          for (let i=0; i<state.income.length; i++) {
            temp += state.income[i].value;
          }
        }
        return temp;
      })
    });

    function AddIncome(data) {
      let d = data.date.split("-");
      let newD = new Date(d[0], d[1], d[2]);

      console.log(data);
      state.income = [...state.income, {
        id: Date.now(), 
        desc: data.desc,
        value: parseInt(data.value),
        date: newD.getTime()
      }];

      console.log(state.income);
    } 

    return {
      Header,
      Form,
      state,
      AddIncome,
      IncomeList
    }
  }
}
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
}

body {
  background: #EEE;
}
</style>
