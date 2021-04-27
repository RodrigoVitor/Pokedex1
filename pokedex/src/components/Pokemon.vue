<template>
    <div>
        <p>{{num}} {{name | upper}}</p>
        <small> {{url}} </small>
    </div>
</template>


<script>
export default {
    props: {
        num: Number,
        name: String,
        url: String
    },
    filters: {
        upper:  function(value) {
            let newName = value[0].toUpperCase() + value.slice(1)
            return newName
          }
    }
}
</script>