<template>
<div class="search-container">
    <label v-if="label">{{ label }}</label>
    <div class="input-wrapper">
        <input
            :value="modelValue"
            @input="$emit('update:modelValue', $event.target.value)"
            :placeholder="placeholder"
            class="search-input"
            type="text"
        />
        <button
            v-if="modelValue"
            @click="$emit('update:modelValue', '')"
            class="clear-btn"
        >
            ✕
        </button>
    </div>

    <!-- Дополнительные события -->
    <div class="search-actions">
        <button @click="$emit('search')" class="action-btn search-btn">Найти</button>
        <button @click="$emit('reset')" class="action-btn reset-btn">Сбросить</button>
    </div>
</div>
</template>

<script>
export default {
    name: 'SearchInput',

    // Специальные пропсы для v-model
    props: {
        modelValue: {
            type: String,
            default: ''
        },
        label: {
            type: String,
            default: ''
        },
        placeholder: {
            type: String,
            default: 'Поиск...'
        }
    },
    
    // Можно определить эмитируемые события
    emits: ['update:modelValue', 'search', 'reset']
}
</script>

<style scoped>
.search-container {
    margin: 20px 0;
}

.input-wrapper {
    position: relative;
    margin: 10px 0;
}

.search-input {
    width: 100%;
    padding: 12px 40px 12px 15px;
    border: 2px solid #ddd;
    border-radius: 8px;
    font-size: 16px;
    transition: border-color 0.3s;
}

.search-input:focus {
    outline: none;
    border-color: #007bff;
}

.clear-btn {
    position: absolute;
    right: 10px;
    top: 50%;
    transform: translateY(-50%);
    background: none;
    border: none;
    font-size: 20px;
    cursor: pointer;
    color: #999;
}

.clear-btn:hover {
    color: #333;
}

.search-actions {
    display: flex;
    gap: 10px;
    margin-top: 10px;
}

.action-btn {
    padding: 10px 20px;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-size: 14px;
    font-weight: bold;
    transition: background-color 0.3s;
}

.search-btn {
    background-color: #28a745;
    color: white;
}

.search-btn:hover {
    background-color: #218838;
}

.reset-btn {
    background-color: #6c757d;
    color: white;
}

.reset-btn:hover {
    background-color: #5a6268;
}
</style>