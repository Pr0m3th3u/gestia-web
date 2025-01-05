<template>
  <div>
    <h1>Your Gallery</h1>
    <ul class="thumbnail-list">
      <li v-for="item in items" :key="item.id" class="thumbnail-item">
        <img :src="item.url" alt="Image" class="thumbnail" />
      </li>
    </ul>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import axios from 'axios';

export default {
  setup(_, { expose }) {
    const items = ref([]);

    const fetchItems = async () => {
      try {
        const response = await axios.get('http://localhost:9090/v1/images/?limit=100');
        items.value = response.data;
      } catch (error) {
        console.error('Fetch data error:', error);
      }
    };

    onMounted(fetchItems);
    expose({ fetchItems });
    return { items };
  },
};
</script>

<style scoped>
.thumbnail-list {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  list-style: none;
  padding: 0;
  margin: 0;
}

.thumbnail-item {
  width: 120px;
  height: 120px;
  border: 1px solid #ccc;
  border-radius: 4px;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #f5f5f5;
}

.thumbnail {
  max-width: 100%;
  max-height: 100%;
  object-fit: cover;
}
</style>
