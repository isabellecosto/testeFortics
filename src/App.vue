<script setup>
import {onMounted, reactive} from "vue"
import FormComments from "./components/form-comments/form-comments.vue"
import ListComments from "./components/list-comments/list-comments.vue"
import {useLocalStorage} from "./composable/use-localstorage/use-locastorage.js"

const {getItemLocalStorage, setItemLocalStorage} = useLocalStorage()
let listComments = reactive({data:[]})
const addComment = (data) => {
  listComments.data.unshift(data)
  setItemLocalStorage("comments", listComments.data)
}

const initData = () => {
  const commentsData = getItemLocalStorage("comments")
  listComments.data = commentsData ? commentsData : []
  console.log(listComments.data)
}

onMounted(() => {
  initData()
})
</script>

<template>
  <div class="container w-600">
    <FormComments @comments="addComment" /> <!--@ É usado para eventos e p/ ouvir emitters-->
    <ListComments :comments="listComments.data" /> <!-- : É usado para passar dados -->
  </div>
</template>

<style scoped>

</style>
