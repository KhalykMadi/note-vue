<template>
<div class="wrapper">
<div class="wrapper-content">
  <section>
    <div class="container">
        <message :message="message" v-if="message"></message>

        <new-note
        :note="note"
        @addNote="addNote">
        </new-note>
      
        <div class="note-header" style="margin: 36px 0">
          <h1>{{title}}</h1>

          <!-- <p> {{search}} </p> -->
          <search :value="search" placeholder="Find your note" @search="search = $event"></search>

          <div class="note-icons">
            <svg :class="{active: grid}" @click="grid = true" style="cursor: pointer"  xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
            <svg :class="{active: !grid}" @click="grid = false" style="cursor: pointer;" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
          </div>
        </div>

        <notes-list :notes="notesFilter" :grid="grid"></notes-list>

    </div>
  </section>
</div>
</div>
</template>

<script>
import Message from '@/components/Message.vue'
import NewNote from '@/components/NewNote.vue'
import NotesList from '@/components/NotesList.vue'
import Search from '@/components/Search.vue'
export default {
  data() {
        return {
         title: 'Notes App',
         grid: true,
         search: '',
         message: null,
         note: {
            title: '',
            descrip: ''
         },
         notes: [
            {
                title: 'First Note',
                descrip: 'Description for first note',
                date: new Date(Date.now()).toLocaleString()
            },
            {
                title: 'Second Note',
                descrip: 'Description for second note',
                date: new Date(Date.now()).toLocaleString()
            },
            {
                title: 'Third Note',
                descrip: 'Description for third note',
                date: new Date(Date.now()).toLocaleString()
            }
         ]
        }
    },
    methods: {
        addNote(){
            let {title, descrip} = this.note
            if(title === '') {
                this.message = 'title can`t be blank'
                return false
            }

            this.notes.push({
                title,
                descrip,
                date: new Date(Date.now()).toLocaleString()
            })
            this.note.title = ''
            this.note.descrip = ''
            this.message = null
        }
    },
    computed: {
      notesFilter(){
        let array = this.notes
        let search = this.search
        if(!search) return array
        // small
        search = search.trim().toLowerCase()
        // filter
        array = array.filter((item) => {
          if(item.title.toLowerCase().indexOf(search) !== -1){
            return item
          }
        })

        return array
      }
    },
  components: {
    Message,
    NewNote,
    NotesList,
    Search
  }
 
}
</script>

<style>
  
</style>
