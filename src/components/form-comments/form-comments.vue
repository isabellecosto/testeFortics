<script setup>
import { defineEmits, ref, computed, watch } from "vue"

const emit = defineEmits(["comments"])

const commentName = ref("")
const commentText = ref("")
const maxCharacterComments = 145
const minCharacterComments = 10
const minCharacterName = 3

const isDisableSendButton = computed(()=> commentText.value.length < minCharacterComments  || commentName.value < minCharacterName) 
const totalCharacter = computed(() => "Total de caracteres: " + commentText.value.length)

watch(commentText, (newValue) => {
    commentText.value = newValue.slice(0, maxCharacterComments)
})

const sendComments = () => {
    const date = new Date()
    const currentDate = date.toLocaleString('pt-BR', {
        year: 'numeric',
        month: '2-digit',
        day: '2-digit',
        hour: '2-digit',
        minute: '2-digit'
        
    });
    const data = {
        name: commentName.value,
        text: commentText.value,
        timestamp: currentDate
    }

    emit("comments", data)
    resetForm()
}

const resetForm = () => {
    commentName.value = ""
    commentText.value = ""
}

</script>
<template>
<link rel="stylesheet" href="form-comments.scss">
<form @submit.prevent class="w-300 padding-md">
    <div class="form-controll">
        <input type="text" name="name" id="name" placeholder="Nome de usuário" v-model="commentName" >
    </div>
    <div class="form-controll">
        <textarea name="comments" placeholder="Digite seu comentário" v-model="commentText" wrap="hard" rows="4"
        cols="50"></textarea>
    </div>
    <div class="form-controll">
        <small>{{ totalCharacter }}</small>
        <button @click="sendComments" :disabled="isDisableSendButton" class="btn">Comentar</button>
    </div>
    <h3>Comentários</h3>
</form>


</template>

<style lang="sass">
@import "form-comments.scss"
</style>