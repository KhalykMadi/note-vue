@<template>
   <div class="new-note">
        <label>Title</label>
        <input v-model="note.title" type="text">
        <label for="">Description</label>
        <textarea v-model="note.descrip"></textarea>
        <button class="newNoteBtn btn btnPrimary" @click="$emit('addNote')">Add</button>
    </div>
</template>

<script>
export default {
    emits: ['addNote'],
    props: {
        note: {
            type: Object,
            required: true
        }
    }
}
</script>

<style lang="scss" scoped>
    .new-note{
        padding: 40px 0;
        text-align: center;
    }
    .newNoteBtn{
        margin-top: 20px;
    }
</style>