<template>
  <div class="relative h-screen">
    <v-modal v-if="showModal">
      <div style="width:750px" class="content p-4">
       
        <div v-if="!isUpdate" class=" flex flex-col space-y-3">
          <input type="text" v-model="note.title" placeholder="titre de la note " class="border border-gray-900  px-3 py-2 text-sm w-full">
          <textarea name="note" @keyup.enter="addNotes" v-model.trim="note.content" id="note" cols="30" rows="10" placeholder="contenu de la note" class="border border-gray-900  px-3 py-2 text-sm w-full"></textarea>
          <p v-if="errorMessage" class="text-red-500"> {{ errorMessage }} </p>
          <v-button @click="addNotes" bgColor="bg-blue-500">ajouter une note</v-button>
          <v-button @click="closeModal" bgColor="bg-red-500">fermer</v-button>
        </div>
        <div v-else class=" flex flex-col space-y-3">
          <input type="text" v-if="saveUpdate" v-model="saveUpdate.title" placeholder="titre de la note " class="border border-gray-900  px-3 py-2 text-sm w-full">
          <textarea name="note" @keyup.enter="updateNote" v-if="saveUpdate" v-model.trim="saveUpdate.content" id="note" cols="30" rows="10" placeholder="contenu de la note" class="border border-gray-900  px-3 py-2 text-sm w-full"></textarea>
          <p v-if="errorMessage" class="text-red-500"> {{ errorMessage }} </p>
          <v-button @click="updateNote" bgColor="bg-blue-500">mise à jour</v-button>
          <v-button @click="closeModal" bgColor="bg-red-500">fermer</v-button>
        </div>
      </div>
    </v-modal>
    <main class="container mx-auto max-w-5xl">
      <div class="flex justify-between items-center py-6">
        <h2 class="text-5xl font-bold ">Notes</h2>
        <button @click="add" class="bg-black text-lg text-white font-semibold rounded-full w-12 h-12">+</button>
      </div>
      <div class="content grid grid-cols-4 gap-4">
        <my-note 
          v-for="(note,index) in notes" 
          :key="index" 
          :note="note"
          @modifier="modifer"
          @supprimer="supprimer"
        ></my-note>
      </div>
    </main>
  </div>
</template>

<script setup lang="ts">
  // les imports 
  import { ref } from 'vue'
  import MyNote from './components/Note.vue'
  import VButton from './components/VButton.vue'
  import VModal from './components/VModal.vue'

  // les types

  import Note from './types/note.interface'


  // les props 




  // les emits 


  //les datas 

  //les datas
  const showModal = ref<boolean>(false) 
  const notes = ref<Note[]>([]) 
  const note = ref({
    title:'' as string,
    content:'' as string,
  })
  const saveUpdate  = ref<Note>()
  const errorMessage = ref<string>("")
  const isUpdate = ref<boolean>(false)


  // les methodes 
  const  getRandomColor = () =>  {
    return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  }
  const closeModal = ()=> {
    showModal.value = false
    note.value.title = ''
    note.value.content = ''
    errorMessage.value = ""
  }
  const add = () => { 
    errorMessage.value = ""
    showModal.value = true
  }
  const addNotes = () => {
    if(note.value.content.length < 10) {
      errorMessage.value = "Le contenu de la note doit depasser 10 caracteres."
    }else {
      isUpdate.value = false
      notes.value.push({
      id:Math.floor(Math.random() * 1000000),
      title:note.value.title,
      content:note.value.content,
      color:getRandomColor(),
      date:new Date()
      })
      showModal.value = false
      note.value.title = ''
      note.value.content = ''
      errorMessage.value = ""
    }
  }

  const modifer =(data:Note) => { 
    isUpdate.value = true
    showModal.value = true
    errorMessage.value= ''
    saveUpdate.value = data
  }

  const updateNote = ()=> {
    
    if(saveUpdate.value && saveUpdate.value.content.length < 10) {
      errorMessage.value = "Le contenu de la note doit depasser 10 caracteres."
    }else {
      for (let index = 0; index < notes.value.length;index++) {
        let note = notes.value[index]
        if(saveUpdate.value) {
          if(note.id ===saveUpdate.value.id) {
            note.title = saveUpdate.value.title
            note.content = saveUpdate.value.content
            notes.value[index].title = note.title
            notes.value[index].content = note.content
            errorMessage.value = '' 
            showModal.value = false
            break
          }
        }
      }
      
     
      
     
      
      
    }
  }
  const supprimer = (data:Note) => {
    notes.value = notes.value.filter(note => note.id  != data.id)
  }





  // les fonctions 








</script>

<style scoped>

</style>