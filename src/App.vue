<template>
  <div id="app">
    <div class="appWrapper">

      <span>
        <input 
          type="date" 
          name="startDate" 
          id="startDate"
          onkeydown="return false"
          v-model="startDate">
      </span>

      <span>
        <input 
          type="date" 
          name="endDate" 
          id="endDate" 
          onkeydown="return false"
          v-model="endDate"
          :min="startDate"
          :disabled=isStartDateSelected>
      </span>
      
      <input 
        type="submit" 
        class="calculate-nbr-days" 
        value="OK"
        v-on:click="calculateDaysNbr"
        :disabled=isStartAndEndDatesAreSelected>

      <div class="msg">
        {{ message }}
      </div>

    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data: function() {
    return {
      startDate: new Date().toISOString().slice(0, 10),
      endDate: this.startDate,
      message: "Choose the start and end dates first!!"
    }
  },
  computed: {
    isStartDateSelected() {
      return this.startDate == null;
    },
    isStartAndEndDatesAreSelected() {
      return this.startDate == null || this.endDate == null;
    }
  },
  watch: {
    startDate() {
      this.endDate = this.startDate;
    }
  },
  methods: {
    calculateDaysNbr() {
      var t1 = (new Date(this.startDate)).getTime();
      var t2 = (new Date(this.endDate)).getTime();
      var nbrDays = parseInt((t2-t1)/(24*3600*1000));
      var appendedMsg = nbrDays<=1? " Day":" Days";
      this.message =  nbrDays +  appendedMsg;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#app .appWrapper > span {
  display: inline-block;
  padding: 10px;
}

#app .appWrapper > span > input {
  padding: 3px;
}

#app .appWrapper input.calculate-nbr-days {
  padding: 5px 8px;
}

#app .appWrapper .msg {
  padding: 20px;
  font-size: 21px;
}

</style>
