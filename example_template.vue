<template>
<form @submit.prevent="submit">
	<input type="text" 
        :id ="uIndx"                                     
        :value= "user.name"                                      
        @input ="addName"  />

    <input type="text" 
        :model-value= "form.name" 
        @update:model-value="form.name = $event"
        v-bind:value="user.name"                                      
        @input="$emit('update:modelValue', $event.target.value)" />   
        <!-- @update:model-value="form.name = $event" -->
    <input :value="user.name" @change = "form.name = $event.target.value" />
    <input type="text" :value="user.name" @input="e => form.name = e.target.value">

</form>	
</template>
<script >
 import { reactive } from '@vue/reactivity'
//  import { reactive } from 'vue'
 import { Inertia } from '@inertiajs/inertia'
import { watchEffect } from '@vue/runtime-core'
 export default {
 // look at the example given in 
 // https://gist.github.com/ErikCH/97e36f02bcdf856686a210e8361a6e91

 props: {
        user: Array
        //User is an Array   with name etc . This props value is given in main property  
      },

      setup(){
       const form  =reactive({
          name :  "",
          email:  "",
          action: ""  
       })
        function submit(event) {
            const {name, email, action } = Object.fromEntries(new FormData(event.target));
             form.name =name, 
             form.email = email 
             form.action = action 
              Inertia.post('/user_roles', form)
        }
        // watchEffect(() => console.log("Value: " + form.vname))
        return { form, submit }

   },
   
   methods:{ 
       addName ($event,$user){
           this.form.name = parseInt($event.target.value);
           console.log($event.target.value); 
       }
   } 

 }

</script>