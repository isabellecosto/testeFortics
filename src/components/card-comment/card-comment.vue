<script setup>
const propsComment = defineProps(["comment"])
</script>

<template>
<div class="card">
    <div class="card-name-data">
        <div class="card-name">
            {{ propsComment.comment.name }}
        </div>
        <div class="card-data">
            {{ propsComment.comment.timestamp }}
        </div>
    </div>
    <div class="card-text">
        {{ propsComment.comment.text }}
    </div>
</div>
</template>

<style lang="sass">
@import "card-comment.scss"
</style>