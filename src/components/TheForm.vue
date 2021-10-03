<template>

  <!-- 1 -->
  <!-- when creating a form it is good to add @submit.prevent in from and use @click in save method taht way if you have any button or will have in future in from that button will not refresh the page and also by adding @click on save button and not in @submit we are defing the button on which click the form will submit it incress readablity when we have very big and complex form-->
  <form @submit.prevent>

    <!-- 2 -->
    <!-- hear we can get input value in 2 ways by @input and by v-model in @input we will just get value we right in input fild and it's not easy to change value of input from code but @input is usefull when we don't want to allow chnage on input value from code and also on every input we want to do somthing. by v-model we are creating 2 way binding that mins when input change in html it will be change in data and when it will change from data it will also affect in html. v-model is very usefull for 2 way bindings and we most offen use v-model -->
    Name: <input type="text" v-model="userForm.name" />   

    <!-- 5 -->
    <!-- just see clg on save method it will show type of age as number but as you know every input value we will get will be type of string only so why we get number hare because we define type number hear and because of that v-model automatically converts value as number and give it to you and that will not be the canse if we get value from @input or ref we have to convert it by our own and it's small but inportant thing to keep in mind because it can lead use to bugs-->
    <!-- and also what to do when we not want to define type of type as number how at that time we can use modifires avalable in v-model cals number like v-model.number this will convert value as number and give it to you so it's alwase good practic to use number modifire in all v-models where you only except nember valuse watcher you use type="number" or not. -->
    <!-- we also have lazy modifire which will not set new value to data on every key strok it will set new value after blur evevt -->
    <!-- and trim modifire will trim white spaces from both side of input value -->
    age: <input type="number" v-model="userForm.age" />

    <!-- 6 -->
    <!-- in select v-model works just like same we define v-model in select and give options value now when user select any optionfrom slelct then the value of that option will be set in data property-->
    <!-- most of the time in select we use options list data's id which we get from response as value and text as text in option but we can also use strings for value as well like we can use names we define between option tag also as value and then on select of any option the data which will be set in data property will be name as well-->
    Friends : <select v-model="userForm.friend">
      <option value="1">vatsal</option>
      <option value="2">shivam</option>
      <option value="3">shubham</option>
    </select>

    <!-- 8 -->
    <!-- keep in mind that when we work with radio and checkbox all matters is how we give them a name and value property -->
    male <input type="radio" name="gender" value="1" v-model="userForm.gender" />
    female <input type="radio" name="gender"  value="2" v-model="userForm.gender" />
    other <input type="radio" name="gender" value="3" v-model="userForm.gender" />

    <!-- 9 -->
    <!-- when working with checkboxes we have 2 options single checkbox and checkbox group  -->
    <!-- vue will identify checkbox is single of group by name we use in checkbox if same name is repating in multiple checkbox then it's group and if name use only once then it's single and base on that it will behive diffrently -->
    <!-- single -->
    conform: <input type="checkbox" name="conform" v-model="userForm.conform" />

    <!-- group -->
    <!-- 11 -->
    <!-- because we are creating checkbox group we have to give them same name to show them as group in vue and html and all should have diffrent value to identify which one of them are selected we give them same v-modle -->
    <p> intrest </p>
    swim <input type="checkbox" name="intrest" value="1" v-model="userForm.intrest" />
    yoga <input type="checkbox" name="intrest" value="2" v-model="userForm.intrest" />
    travle <input type="checkbox" name="intrest" value="3" v-model="userForm.intrest" />

    <!-- 14 -->
    <!-- don't you think it will be great if we can make our custome component and can use v-model to it and can use that component of form -->
    <!-- basically there are 2 ways to achive that one is use props and events in child component and base on that update value of that component in user from or if we can use v-model somehow on the custom component -->
    <!-- we can use v-model on component and vue will do that props and events thing behind the seen for us -->
    <Rating  v-model="userForm.rating" />  
    <!-- when you define v-modle on component vue will do somthing like this 
    <Rating  :modelValue="userForm.rating" @update:model-value="set new value as userForm.rating" />  so it's just like creating props and emit by our won hear by using v-model we are using vue's defined props and emits-->
    <!-- but we should only use this when we want to create some custome input elements not in all components where we want to pass props and emit data -->

    <!-- 3 -->
    <!-- hear we are calling save method which will be responsbile for doing things which we want to do in from submit -->
    <button @click="saveUser"> Save </button>
  </form>  

</template>

<script>

import Rating from './Rating.vue';

export default {

  components: {
    Rating
  },

  data(){
    return{

      // 4
      // it is good practic to group all from related data in one object and postfix it whit 'form' insted of creating individual data properties 
      userForm: {
        name: '',
        age: null,
        // 7
        // most of the time we create any select with some pre selected value so we can do it hear by giving friend any pre selected value
        // also keep in mind hear we are using number as option value so because of taht 2 and '2' will be treated as same both select shivam but when we sumit form without changing select we will get type number and if we change value we will get type string because options there is in string so to avoid that small but you can set perdefine value hear as '' of if you are just working with ids as option value you just use number modifire in v-modle in select to enshoure that if we change predefine value of not we will get same type alwase
        friend: 2,
        gender: null,

        // 10 
        // when we are creating single checkbox vue will give us value of that in boolean so hear we are setting it as false to uncheckde initially and we don't need to provode value in single checkbox in html because they will be true of false just never use [] as initial for single checkbox because it will be use in checkbox group and vue will behave unexpectedly when we use [] for single checkbox. 
        conform: false,

        // 12
        // because we are creating hear group checkbox where we want to allow user to check multiple values we have to give vue hint that it's group chjeckbox for that we have to give them same name in html to show them as group and give them same v-modle to bind it to single data and also that idat has to be in [] otherwise it won't work because vue will add all selected checkbox's values in that array and vue have to know that it's group checkbox so it has to be type of array [] array or [1,3] (pre selected) not matter but it has to be array
        // now vue will add all selected checkbox values in array
        intrest: [],
        rating: 3
      }
    };
  },

  methods: {
    saveUser(){
      console.log('form', this.userForm);
      console.log('type of age', typeof this.userForm.age)
    }
  }

};

</script>

<style scoped>

</style>