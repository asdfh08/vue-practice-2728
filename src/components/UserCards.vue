<template>
<div class="user-cards-demo">
    <h2>Пример 4: Компоненты и пропсы</h2>
    <p>Демонстрация передачи данных через пропсы и использование слотов</p>

    <div class="cards-container">
        <!-- Передаем данные через пропсы -->
        <UserCard
            :user="adminUser"
            :is-active="true"
            @user-clicked="handleUserClick"
        >
            <!-- Именованный слот -->
            <template #actions>
                <button @click="editUser(adminUser)" class="edit-btn">Редактировать</button>
            </template>

            <!-- Слот по умолчанию -->
            <p>Администратор системы с полными правами доступа</p>
        </UserCard>

        <!-- Динамический рендеринг списка пользователей -->
        <UserCard
            v-for="user in users"
            :key="user.id"
            :user="user"
            @user-clicked="handleUserClick"
        >
            <template #actions>
                <button @click="editUser(user)" class="edit-btn">Редактировать</button>
                <button @click="deleteUser(user.id)" class="delete-btn">Удалить</button>
            </template>
        </UserCard>
    </div>

    <div class="debug-info">
        <h3>Действия:</h3>
        <p>Клики по пользователям: {{ clickLog.length }}</p>
        <ul>
            <li v-for="(log, index) in clickLog" :key="index">
                Клик по: {{ log.name }} ({{ log.email }})
            </li>
        </ul>
    </div>
</div>
</template>

<script>
import UserCard from './UserCard.vue'

export default {
    name: 'UserCards',
    
    components: {
        UserCard
    },
    
    data() {
        return {
            adminUser: {
                id: 1,
                name: 'Анна Иванова',
                email: 'anna@example.com',
                role: 'admin'
            },
            
            users: [
                {
                    id: 2,
                    name: 'Петр Сидоров',
                    email: 'petr@example.com',
                    role: 'user'
                },
                {
                    id: 3,
                    name: 'Мария Петрова',
                    email: 'maria@example.com',
                    role: 'user'
                },
                {
                    id: 4,
                    name: 'Иван Кузнецов',
                    email: 'ivan@example.com',
                    role: 'user'
                }
            ],
            
            clickLog: []
        }
    },
    
    methods: {
        handleUserClick(user) {
            this.clickLog.push(user)
            console.log('Клик по пользователю:', user)
        },
        
        editUser(user) {
            alert(`Редактирование пользователя: ${user.name}`)
            console.log('Редактирование:', user)
        },
        
        deleteUser(userId) {
            if (confirm('Удалить пользователя?')) {
                this.users = this.users.filter(user => user.id !== userId)
            }
        }
    }
}
</script>

<style scoped>
.user-cards-demo {
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
}

.cards-container {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    margin: 20px 0;
}

.edit-btn {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    margin-right: 10px;
}

.delete-btn {
    background-color: #dc3545;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
}

.debug-info {
    margin-top: 30px;
    padding: 20px;
    background-color: #f8f9fa;
    border-radius: 8px;
    border: 1px solid #ddd;
}

.debug-info ul {
    list-style-type: none;
    padding: 0;
}

.debug-info li {
    padding: 5px 0;
    border-bottom: 1px solid #eee;
}
</style>