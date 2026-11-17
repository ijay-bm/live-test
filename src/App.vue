<script setup lang="ts">
import { ref } from 'vue'

const petName = ref('')

const pets = ref([])

function addPet() {
  if (petName.value.trim() !== '') {
    pets.value.push({
      name: petName.value,
      status: 'listed',
    })
    petName.value = ''
  }
}
</script>

<template>
  <main>
    <div>
      <div class="pet-add-form">
        <label for="petName">Pet Name</label>
        <input v-model="petName" id="petName" placeholder="Enter pet name" />
        <button @click="addPet()">Add pet</button>
      </div>
    </div>

    <div class="pet-lists">
      <div class="pet-list">
        <h1>Listed</h1>
        <div>
          <ul>
            <li v-for="(pet, index) in pets.filter((p) => p.status === 'listed')" :key="index">
              <span>{{ pet.name }}</span>
              <button @click="pet.status = 'examining'">Next</button>
            </li>
          </ul>
        </div>
      </div>

      <div class="pet-list">
        <h1>Examining</h1>
        <div>
          <ul>
            <li v-for="(pet, index) in pets.filter((p) => p.status === 'examining')" :key="index">
              <span>{{ pet.name }}</span>
              <button @click="pet.status = 'finally_back_to_hooman'">Next</button>
            </li>
          </ul>
        </div>
      </div>

      <div class="pet-list">
        <h1>Finally Back to Hooman</h1>
        <div>
          <ul>
            <li
              v-for="(pet, index) in pets.filter((p) => p.status === 'finally_back_to_hooman')"
              :key="index"
            >
              {{ pet.name }}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </main>
</template>

<style>
main {
  max-width: 800px;
  margin: 0 auto;
}

.pet-add-form {
  display: flex;
  justify-content: end;
}

.pet-add-form input {
  margin: 0 10px;
}

.pet-lists {
  display: flex;
  justify-content: space-between;
  margin-top: 20px;
}

.pet-list {
  flex: 1;
  margin: 0 10px;
}

.pet-list li {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
  padding-right: 10px;
}

h1 {
  font-size: 1rem;
}

ul {
  list-style: none;
  padding: 0;
}
</style>
