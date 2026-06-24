<template>
  <div class="app">
    <header class="header">
      <h1>🏡 Homes & Beyond</h1>
      <p>{{ filteredProperties.length }} properties found</p>
    </header>

    <div class="controls">
      <input
        v-model="searchQuery"
        type="text"
        placeholder="Search by title or location..."
        class="search-input"
      />
      <select v-model="sortOrder" class="sort-select">
        <option value="low-to-high">Price: Low to High</option>
        <option value="high-to-low">Price: High to Low</option>
      </select>
    </div>

    <div class="grid">
      <PropertyCard
        v-for="property in filteredProperties"
        :key="property.id"
        :property="property"
        @toggle-bookmark="toggleBookmark"
      />
    </div>
  </div>
</template>

<script>
import PropertyCard from './components/PropertyCard.vue'

export default {
  name: 'App',
  components: { PropertyCard },
  data() {
    return {
      searchQuery: '',
      sortOrder: 'low-to-high',
      properties: [
        { id: 1, title: 'Clifton Sea-View Apartment', location: 'Clifton, Cape Town', price: 3500, type: 'Apartment', image: 'https://images.unsplash.com/photo-1560448204-e02f11c3d0e2?w=400&h=250&fit=crop', available: true, bookmarked: false },
        { id: 2, title: 'Camps Bay Beach Cottage', location: 'Camps Bay, Cape Town', price: 5200, type: 'Cottage', image: 'https://images.unsplash.com/photo-1499793983690-e29da59ef1c2?w=400&h=250&fit=crop', available: true, bookmarked: false },
        { id: 3, title: 'Bo-Kaap Studio', location: 'Bo-Kaap, Cape Town', price: 1800, type: 'Studio', image: 'https://images.unsplash.com/photo-1522708323590-d24dbb6b0267?w=400&h=250&fit=crop', available: false, bookmarked: false },
        { id: 4, title: 'Green Point Loft', location: 'Green Point, Cape Town', price: 2900, type: 'Loft', image: 'https://images.unsplash.com/photo-1493809842364-78817add7ffb?w=400&h=250&fit=crop', available: true, bookmarked: false },
        { id: 5, title: 'Hout Bay Villa', location: 'Hout Bay, Cape Town', price: 7800, type: 'Villa', image: 'https://images.unsplash.com/photo-1512917774080-9991f1c4c750?w=400&h=250&fit=crop', available: false, bookmarked: false },
        { id: 6, title: 'Observatory Garden Flat', location: 'Observatory, Cape Town', price: 1500, type: 'Flat', image: 'https://images.unsplash.com/photo-1484154218962-a197022b5858?w=400&h=250&fit=crop', available: true, bookmarked: false }
      ]
    }
  },
  computed: {
    filteredProperties() {
      let result = this.properties.filter(p => {
        const query = this.searchQuery.toLowerCase()
        return (
          p.title.toLowerCase().includes(query) ||
          p.location.toLowerCase().includes(query)
        )
      })
      if (this.sortOrder === 'low-to-high') {
        result.sort((a, b) => a.price - b.price)
      } else {
        result.sort((a, b) => b.price - a.price)
      }
      return result
    }
  },
  methods: {
    toggleBookmark(id) {
      const property = this.properties.find(p => p.id === id)
      if (property) property.bookmarked = !property.bookmarked
    }
  }
}
</script>