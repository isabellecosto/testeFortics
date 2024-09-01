<script setup>
import { defineEmits, ref, computed, watch } from "vue"

const emit = defineEmits(["comments"])

const commentName = ref("")
const commentText = ref("")

const isDisableSendButton = computed(()=> commentText.value.length < 10)
const totalCharacter = computed(() => commentText.value.length)
const maxTextComment = computed(()=>{
    if (commentText.value.length > 145) {
        return "Comentário não pode ter mais de 145 caracteres"
    }
    return ""
})

watch(commentText, (newValue) => {
    commentText.value = newValue.slice(0, 145)
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
}

</script>
<template>
<form @submit.prevent>
    <div class="form-controll">
        <label for="name">Nome de usuário</label>
        <input type="text" name="name" id="name" v-model="commentName">
    </div>
    <div class="form-controll">
        <textarea name="comments" v-model="commentText" ></textarea>
    </div>
    <div class="form-controll">
        <small>{{ totalCharacter }}</small>
        <small>{{ maxTextComment }}</small>
        <button @click="sendComments" :disabled="isDisableSendButton">Comentar</button>
    </div>
</form>


</template>
<style lang="sass">

</style>