This repo explains an alternative to Vue-model.
We use v-model in the following situation 

```
<div>
<input v-model ="myvar" value="test"> 
{{myvar}}
</div>
<script>
export default{
    data (){
        return {
            mvar : String 
        }
    }

}
</script>
```
We use v-model for a two way binding. However sometimes we need to determine the binding value by programs and it not known before the program starts. So we need to bind the value with v-bind and at the same time use v-model for the input field.  This repo  has an example to explain how to use v-model and v-bind at the same time. 


