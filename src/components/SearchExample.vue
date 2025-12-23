<template>
<div class="search-example">
    <h2>Пример 5: Поиск и кастомные элементы</h2>
    <p>Демонстрация кастомного компонента с v-model</p>

    <!-- Используем кастомный v-model -->
    <SearchInput
        v-model="searchQuery"
        label="Поиск по имени:"
        placeholder="Введите имя пользователя..."
        @search="performSearch"
        @reset="resetSearch"
    />

    <div class="search-info">
        <p>Текущий запрос: "<strong>{{ searchQuery }}</strong>"</p>
        <p>Найдено пользователей: {{ searchResults.length }}</p>
    </div>

    <div v-if="searchResults.length" class="results-container">
        <h3>Результаты поиска:</h3>
        <div class="results-grid">
            <div v-for="user in searchResults" :key="user.id" class="user-card">
                <h4>{{ user.name }}</h4>
                <p>{{ user.email }}</p>
                <p class="user-bio">{{ user.bio }}</p>
            </div>
        </div>
    </div>

    <div v-else-if="searchQuery" class="no-results">
        <p>Пользователи по запросу "{{ searchQuery }}" не найдены</p>
    </div>

    <div v-else class="all-users">
        <h3>Все пользователи:</h3>
        <div class="results-grid">
            <div v-for="user in users" :key="user.id" class="user-card">
                <h4>{{ user.name }}</h4>
                <p>{{ user.email }}</p>
            </div>
        </div>
    </div>
</div>
</template>

<script>
import SearchInput from './SearchInput.vue'
import { ref, computed } from 'vue'

export default {
    name: 'SearchExample',
    
    components: {
        SearchInput
    },
    
    setup() {
        const searchQuery = ref('')
        
        const users = ref([
            { id: 1, name: 'Анна Иванова', email: 'anna@test.com', bio: 'Frontend разработчик' },
            { id: 2, name: 'Борис Петров', email: 'boris@test.com', bio: 'Backend разработчик' },
            { id: 3, name: 'Виктор Сидоров', email: 'victor@test.com', bio: 'Fullstack разработчик' },
            { id: 4, name: 'Дмитрий Кузнецов', email: 'dmitry@test.com', bio: 'DevOps инженер' },
            { id: 5, name: 'Елена Смирнова', email: 'elena@test.com', bio: 'UI/UX дизайнер' },
            { id: 6, name: 'Федор Николаев', email: 'fedor@test.com', bio: 'Тестировщик' }
        ])
        
        const searchResults = computed(() => {
            if (!searchQuery.value.trim()) return []
            
            return users.value.filter(user =>
                user.name.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
                user.email.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
                user.bio.toLowerCase().includes(searchQuery.value.toLowerCase())
            )
        })
        
        const performSearch = () => {
            console.log('Выполняем поиск:', searchQuery.value)
            alert(`Ищем: ${searchQuery.value}`)
        }
        
        const resetSearch = () => {
            searchQuery.value = ''
            console.log('Сброс поиска')
        }
        
        return {
            searchQuery,
            searchResults,
            users,
            performSearch,
            resetSearch
        }
    }
}
</script>

<style scoped>
.search-example {
    max-width: 1000px;
    margin: 0 auto;
    padding: 20px;
}

.search-info {
    margin: 20px 0;
    padding: 15px;
    background-color: #e9ecef;
    border-radius: 8px;
}

.results-container {
    margin-top: 30px;
}

.results-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 20px;
    margin-top: 20px;
}

.user-card {
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 8px;
    background-color: white;
    transition: transform 0.2s, box-shadow 0.2s;
}

.user-card:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.user-card h4 {
    margin: 0 0 10px 0;
    color: #333;
}

.user-card p {
    margin: 5px 0;
    color: #666;
}

.user-bio {
    font-size: 14px;
    font-style: italic;
    color: #888;
}

.no-results, .all-users {
    margin-top: 30px;
    padding: 20px;
    background-color: #f8f9fa;
    border-radius: 8px;
    border: 1px solid #ddd;
}

.all-users h3 {
    margin-top: 0;
}
</style>