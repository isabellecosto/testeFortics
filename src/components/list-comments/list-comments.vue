<script setup>
import CardComment from "../card-comment/card-comment.vue"
import {defineProps} from "vue"
const propsComment = defineProps(['comments'])



</script>
<template>
<div class="list-comments padding-md" v-for="comment in propsComment.comments">
    <!-- {{ propsComment.comments }} -->
    <CardComment :comment="comment" /> 
</div>
</template>
<style lang="sass">

</style>