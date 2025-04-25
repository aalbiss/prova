<script setup>
import { ref } from 'vue'
import { watch } from 'vue'
import VueDatePicker from '@vuepic/vue-datepicker'
import '@vuepic/vue-datepicker/dist/main.css'

const start = ref(null)
const end = ref(null)

// Watcher for the end date
watch(end, (newEnd) => {
  //Check if the end date is less than start date
  if (newEnd && start.value && newEnd < start.value) {
    // Assign the start date as end date minus a day
    const correctedStart = new Date(newEnd)
    correctedStart.setDate(correctedStart.getDate() - 1)
    start.value = correctedStart
  }
})
</script>

<template>
  <div class="font-sans flex justify-center items-center">
    <!-- TODO: redirect to mainpage -->
    <form action="" method="post" class="p-4">
      <div>
        <input
          class="text-lg w-full p-2 mt-4 border border-gray-300 rounded-md"
          type="text"
          id="groupname"
          placeholder="Nome del Gruppo"
        />
        <input
          class="text-lg w-full p-2 mt-4 border border-gray-300 rounded-md"
          type="text"
          id="destination"
          placeholder="Destinazione Viaggio"
        />
      </div>
      <div class="text-lg mt-4 font-medium">Inserisci Date del Viaggio</div>
      <div class="flex gap-4 mt-2">
        <VueDatePicker
          v-model="start"
          :enable-time-picker="false"
          :format="'dd/mm/yyyy'"
          class="w-1/2"
          placeholder="Inizio"
        ></VueDatePicker>
        <VueDatePicker
          v-model="end"
          :enable-time-picker="false"
          :format="'dd/mm/yyyy'"
          class="w-1/2"
          placeholder="Fine"
        ></VueDatePicker>
      </div>
      <br />
      <div class="flex justify-center">
        <button
          class="w-1/3 bg-MediumPurple-500 text-white text-lg py-3 rounded-xl hover:opacity-90 transition duration-200 transform hover:-translate-y-0.5 shadow-lg hover:shadow-xl"
          type="submit"
        >
          Invio
        </button>
      </div>
    </form>
  </div>
</template>
