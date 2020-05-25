<template>

  <div class="hello">
    <div class="heartbeat">
      <img src="../assets/cardiology.svg" alt="">
    </div>
      
    <h1>Vue.js Calorie Counter</h1>
    <div class='columnNames'>
        <span>DESCRIPTION</span>
        <span>CALORIES</span>
        <span>FAT</span>
        <span>CARBS</span>
        <span>PROTEIN</span>
    </div>
 <ul>
   <li v-for="(item, index) in listOfItems" v-bind:key="index">
   <span>{{ item.name}}</span>
   <span>{{ item.calories}}</span>
   <span>{{ item.carbs}}</span>
   <span>{{ item.fat}}</span>
   <span>{{ item.prot}}</span>
   &nbsp;
   <button v-on:click="removeItem(index)">x</button>
   </li> 
 </ul>

<div class="totals">
  <span>Totals:</span>
  <span>{{ totals.totalCal}}</span>
  <span>{{ totals.totalCarbs}}</span>
  <span>{{ totals.totalFat}}</span>
  <span>{{ totals.totalProt}}</span>
</div>

 <div class=sum>
    <input v-bind:placeholder="placeholderValues.inputNameText" v-model="newValues.newName" type="text">
      <input v-bind:placeholder="placeholderValues.inputCalorieText" v-model="newValues.newCalories" type="number">
      <input v-bind:placeholder="placeholderValues.inputCarbsText" v-model="newValues.newCarbs" type="number">
      <input v-bind:placeholder="placeholderValues.inputFatText" v-model="newValues.newFat" type="number">
      <input v-bind:placeholder="placeholderValues.inputProteinText" v-model="newValues.newProtein" type="number">
   <button v-on:click="addItem">+</button>
 </div>

  </div>
  
</template>

<script>
export default {
  name: 'HelloWorld',
  data: function () {
    return {
      placeholderValues: {
        inputNameText:'Description',
       inputCalorieText: 'Calories',
        inputCarbsText:'Fat',
         inputFatText:'Carbs',
          inputProteinText:'Protein'
          },
         newValues: {
      newName:'',
      newCalories:'',
      newCarbs:'',
      newFat:'',
      newProtein:''
      },
      
      listOfItems:[
        {

          name: 'This is an item',
          calories: 1000,
          carbs: 500,
          fat: 10,
          prot: 100
        },
         {
          name: 'This is also an item',
          calories: 1000,
          carbs: 500,
          fat: 10,
          prot: 100
        },
      
       {
          name: 'Hey, me too',
          calories: 1000,
          carbs: 500,
          fat: 10,
          prot: 100
        }
      
      ],
      totals:{
        totalCal:0,
        totalCarbs:0,
        totalFat:0,
        totalProt:0
      }
    }
    },
    methods: {
      addItem: function(){
        this.listOfItems.push({
          name: this.newValues.newName,
        calories: this.newValues.newCalories,
        carbs: this.newValues.newCarbs,
        fat: this.newValues.newFat,
        prot: this.newValues.newProtein,
        });
        this.newValues.newName = null,      
      this.newValues.newCalories = null,  
      this.newValues.newCarbs = null,
      this.newValues.newFat = null,
      this.newValues.newProtein = null,
      this.calcValues()
    },
    removeItem: function(itemIndex){
      this.listOfItems.splice(itemIndex, 1);
      this.calcValues()


    },
    calcValues: function(){
     
        this.totals.totalCal = 0;
        this.totals.totalCarbs = 0;
        this.totals.totalFat = 0;
        this.totals.totalProt = 0;

      for(let i = 0; this.listOfItems.length; i++){ 
        
        this.totals.totalCal += parseInt(this.listOfItems[i].calories); 
        this.totals.totalCarbs += parseInt(this.listOfItems[i].carbs);
        this.totals.totalFat += parseInt(this.listOfItems[i].fat);
        this.totals.totalProt += parseInt(this.listOfItems[i].prot);
      }

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

body{
  margin:0;
  padding:0;
  
}

.hello{
 border: 40px solid rgb(18, 172, 107);
 margin: 0 auto;
 text-align: center;
 width:650px;
 min-height: 410px;
 max-height:600px;
margin-top:50px;
font-family: 'Calibri';
color:rgb(192, 191, 189);


img{
  width:100px;
  margin-left: -550px;
  margin-top: -25px;
}

.heartbeat{
    height:70px;
    width:100% ;
    position: relative;
    background-color: #009788;
}
 h1{
   font-family: 'Arial';
   font-weight: 10;
   color:rgb(243, 237, 237);
   position:absolute;
   top:90px;
   left:620px;
 }

 .columnNames {

  display:flex;
  justify-content: space-between;
   border-bottom:1px solid rgb(243, 237, 237);
   color:rgb(48, 45, 45);
   font-weight:bold;


   span{
     display: inline-block;
     margin-left: 20px;
     padding:20px;
     
     
   }
 }

 ul {
      padding:0;
      margin-left:-15px;
      padding:10px 50px;
      padding-left:10px;
      position: relative;

    
      li{
        list-style-type: none;
        display:flex;
        justify-content: space-between;
        
    
        
        span {
          display:inline-block;
          padding:5px;
          border-bottom: 1px solid rgb(243, 237, 237);
          &:nth-child(1){
            width:25%;
          }
        }
   }
     button{
        border:none;
        background-color: #fff;
        color:rgb(216, 208, 208);
        font-size: 15px;
        font-weight: bold;
        position:absolute;
        left:625px;
        // top:-20px;
        cursor: pointer;


      }

 }

.totals{


  display:flex;
      justify-content: space-between;
      background-color:#e7e7e7;
      padding:20px;
      
      span {
        display: inline-block;
        padding-left: 5px;
        width:100px;
        font-weight: bold;
        font-size:25px;
        color:rgb(63, 60, 60);
        &:nth-child(1){
          width:25%;
          
        }
      }
    }

.sum{

       display: flex;
      justify-content: space-between;
      padding:20px;
      padding-bottom: 30px;
      position: relative;
      

      input {
        border:none;
        border-bottom:1px solid rgb(145, 140, 140);
        width:100px;
        padding:5px 0 5px 5px;
        display:inline-block;
        &:nth-child(1){
            width:25%;
          }
        
      }
      

  button{
    width:60px;
    height:60px;
    border-radius: 50%;
    background-color: #019784;
    border:none;
    color:#fff;
    font-size: 50px;
    font-weight: bold;
    position:absolute;
    top:50px;
    left:615px;
    cursor: pointer;
  }
}

}



</style>

