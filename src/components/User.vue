<template>
    <tr >
        <th scope="row">{{user.Id}}</th>
        <td>{{user.Name | capitalize}}</td>
        <td>{{user.Mail}}</td>
        <td>{{user.Age}}</td>
    </tr>
</template>

<script>
export default {
    props:["user"],
    filters:{
        capitalize: function (value) {
            if (!value) return ''
            value = value.toString()
            return value.charAt(0).toUpperCase() + value.slice(1)
        }
    }
}

</script>

<style scoped>

</style>