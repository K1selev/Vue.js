<template>
  <div id="app">
    <div class="price-list">
      <h1>Услуги</h1>
      <div
        v-for="(service, index) in services"
        :key="service.name"
        :class="['service-item', { selected: service.selected, inactive: !service.selected }]"
        @click="toggleSelection(index)"
      >
        <div class="service-info">
          <h3>{{ service.name }}</h3>
          <p class="price">${{ formatPrice(service.price) }}</p>
        </div>
      </div>
      <div class="total">
        <h2>Итого: ${{ formatPrice(totalSum) }}</h2>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      services: [
        { name: 'Веб-разработка', price: 300, selected: false },
        { name: 'Дизайн', price: 400, selected: false },
        { name: 'Интеграция', price: 250, selected: false },
        { name: 'Обучение', price: 220, selected: false }
      ]
    };
  },
  computed: {
    totalSum() {
      return this.services.reduce((sum, service) => {
        return service.selected ? sum + service.price : sum;
      }, 0);
    }
  },
  methods: {
    toggleSelection(index) {
      this.services[index].selected = !this.services[index].selected;
    },
    formatPrice(price) {
  return price.toFixed(2); // Форматируем цену с двумя знаками после запятой
    }
  }
};
</script>

<style scoped>

#app {
  min-height: 100vh;
  background-color: #5ba3ba;
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  color: white;
  /* display: flex; */
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.price-list {
  text-align: center;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

h1 {
  font-size: 2rem;
  margin-bottom: 20px;
}

.service-item {
  background-color: #f1f1f1;
  margin: 10px 0;
  padding: 20px;
  width: 100%;
  max-width: 500px;
  cursor: pointer;
  transition: none;
  text-align: left;
  color: white;
}

.service-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.service-item h3 {
  font-size: 1.25rem;
  margin: 0;
}

.price {
  font-size: 1rem;
  margin: 0;
}

.service-item.selected {
  background-color: #8ebf74;
}

.service-item.inactive {
  background-color: #e75684;
}
.service-item:hover {
  transform: scale(1.05);
}
.total {
  margin-top: 30px;
  font-size: 1.5rem;
  font-weight: bold;
}
</style>
