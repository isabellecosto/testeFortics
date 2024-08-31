<script setup>
import {ref} from "vue"
import FormComments from "./components/form-comments/form-comments.vue"
import ListComments from "./components/list-comments/list-comments.vue"
const listComments = ref([])
const addComment = (data) => {
  listComments.value.push(data)
  console.log(data)
}
</script>

<template>
  <FormComments @comments="addComment" /> <!--@ É usado para eventos e p/ ouvir emitters-->
  <ListComments :comments="listComments" /> <!-- : É usado para passar dados -->
</template>

<style scoped>

</style>
