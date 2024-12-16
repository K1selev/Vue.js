<template>
  <div id="app">
    <div class="container">
      <h1>Список услуг</h1>
      <div class="search-container">
        <span class="search-icon">🔍</span>
        <input 
          type="text" 
          v-model="searchQuery" 
          placeholder="Поиск услуг..." 
          class="search-box"
        />
      </div>
      <div class="services">
        <div 
          v-for="service in filteredServices" 
          :key="service.id" 
          :class="['service-item', { active: selectedServices.includes(service.id), inactive: !selectedServices.includes(service.id) }]"
          @click="toggleService(service.id)"
        >
          <span class="service-name">{{ service.name }}</span>
          <span class="service-price">{{ service.price.toFixed(2) }} $</span>
        </div>
      </div>
      <div class="total">
        <h2>Итоговая сумма: {{ totalPrice.toFixed(2) }} $</h2>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: "",
      services: [
        { id: 1, name: "Веб-разработка", price: 300 },
        { id: 2, name: "Дизайн", price: 400 },
        { id: 3, name: "Интеграция", price: 250 },
        { id: 4, name: "Обучение", price: 220 },
        { id: 5, name: "Техническая поддержка", price: 150 },
        { id: 6, name: "SEO-оптимизация", price: 500 },
        { id: 7, name: "Мобильная разработка", price: 800 },
        { id: 8, name: "Аудит безопасности", price: 600 },
        { id: 9, name: "Сопровождение проектов", price: 300 },
        { id: 10, name: "Консультация по UX/UI", price: 200 },
        { id: 11, name: "Написание документации", price: 180 },
        { id: 12, name: "Контент-менеджмент", price: 400 },
        { id: 13, name: "QA-тестирование", price: 350 },
        { id: 14, name: "DevOps-настройка", price: 700 },
        { id: 15, name: "Администрирование серверов", price: 450 },
        { id: 16, name: "Перевод веб-контента", price: 100 },
        { id: 17, name: "Автоматизация бизнес-процессов", price: 900 },
        { id: 18, name: "Оптимизация производительности", price: 550 },
        { id: 19, name: "Обучение персонала", price: 250 },
        { id: 20, name: "Разработка чат-ботов", price: 650 },
        { id: 21, name: "Настройка аналитики", price: 300 },
        { id: 22, name: "Брендинг", price: 450 },
        { id: 23, name: "UI прототипирование", price: 280 },
        { id: 24, name: "Разработка e-commerce сайтов", price: 1200 },
        { id: 25, name: "Оптимизация конверсии", price: 320 }
      ],
      selectedServices: []
    };
  },
  computed: {
    filteredServices() {
      return this.services.filter((service) =>
        service.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
    totalPrice() {
      return this.services
        .filter((service) => this.selectedServices.includes(service.id))
        .reduce((sum, service) => sum + service.price, 0);
    }
  },
  methods: {
    toggleService(serviceId) {
      if (this.selectedServices.includes(serviceId)) {
        this.selectedServices = this.selectedServices.filter(
          (id) => id !== serviceId
        );
      } else {
        this.selectedServices.push(serviceId);
      }
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

.container {
  max-width: 600px;
  margin: 0 auto;
  text-align: center;
}

h1 {
  margin-bottom: 40px;
  color: #fff;
}

.search-container {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
  position: relative;
}

.search-icon {
  position: absolute;
  left: 10px;
  font-size: 16px;
  color: #333;
}

.search-box {
  padding: 10px 10px 10px 30px;
  font-size: 16px;
  width: 100%;
  box-sizing: border-box;
}

.services {
  /* margin: 20px 0; */
}

.service-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  margin: 10px 0;
  background: #e75684;
  color: #fff;
  cursor: pointer;
  transition: background 0.3s;
}

.service-item.active {
  background: #8ebf74;
}

.service-name {
  font-weight: bold;
}

.total {
  font-size: 18px;
  font-weight: bold;
  margin-top: 20px;
  margin-bottom: 0px;
}
</style>
