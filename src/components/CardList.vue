<template>
  <header class="header">
    <nav class="header_navigation">
      <div class="button_container">
        <button>Filter 1</button>
        <button>Filter 2</button>
        <button>Filter 3</button>
      </div>
    </nav>
  </header>
  <div class="container">
    <div class="card" v-for="(card, index) in cards" :key="index">
      <h2>{{ card.title }}</h2>
      <p>{{ card.description }}</p>
      <div class="image-placeholder"></div>
      <button>Перейти</button>
    </div>
  </div>
</template>

<style>
.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  width: 100vw;
  padding: 20px 20px;
}

.card {
  background-color: #333;
  color: #fff;
  border-radius: 12px;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.5);
  margin: 16px;
  padding: 16px;
  box-sizing: border-box;
  flex: 1 1 calc(20% - 32px);
  max-width: calc(20% - 32px);
  aspect-ratio: 16 / 9;
}

.card h2 {
  margin: 0 0 8px;
}

.card p {
  margin: 0 0 16px;
}

.image-placeholder {
  background-color: #555;
  width: 100%;
  aspect-ratio: 16 / 9;
  border-radius: 8px;
  margin-bottom: 16px;
}

button {
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 10px 16px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

.header {
  width: 100vw;
}

.header_navigation {
  display: flex;
  justify-content: flex-end;
  padding-right: 36px;
  padding-left: 36px;
  padding-top: 20px;
}

.button_container button {
  margin-left: 8px;
  border: none;
  padding: 10px 33px;
}

.button_container button:first-child {
  margin-left: 0;
}

@media (max-width: 1200px) {
  .card {
    flex: 1 1 calc(25% - 32px);
    max-width: calc(25% - 32px);
  }
}

@media (max-width: 900px) {
  .card {
    flex: 1 1 calc(33.33% - 32px);
    max-width: calc(33.33% - 32px);
  }
}

@media (max-width: 600px) {
  .card {
    flex: 1 1 calc(50% - 32px);
    max-width: calc(50% - 32px);
  }
}

@media (max-width: 409px) {
  .header_navigation {
    justify-content: center;
  }
  .button_container {
    display: flex;
    flex-direction: column;
  }
  .button_container button {
    margin: 8px 0;
  }
}

@media (max-width: 400px) {
  .card {
    flex: 1 1 calc(100% - 32px);
    max-width: calc(100% - 32px);
  }
}
</style>

<script lang="ts">
import { defineComponent, reactive } from 'vue'

class Card {
  title: string
  description: string

  constructor(title: string, description: string) {
    this.title = title
    this.description = description
  }

  static make(n: number): Card[] {
    const cards: Card[] = []
    for (let i = 0; i < n; i++) {
      cards.push(new Card(`Title ${i + 1}`, `Description ${i + 1}`))
    }
    return cards
  }
}

export default defineComponent({
  setup() {
    const cards = reactive<Card[]>(Card.make(10))
    return { cards }
  },
})
</script>
