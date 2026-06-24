<template>
  <div class="card" :class="{ unavailable: !property.available }">
    
    <!-- Not Available Ribbon -->
    <div v-if="!property.available" class="ribbon">Not Available</div>

    <!-- Property Image -->
    <img :src="property.image" :alt="property.title" class="card-image" />

    <!-- Card Body -->
    <div class="card-body">
      <h3 class="card-title">{{ property.title }}</h3>
      <p class="card-location">📍 {{ property.location }}</p>
      <p class="card-type">🏠 {{ property.type }}</p>
      <p class="card-price">R {{ property.price }} / night</p>

      <!-- Bookmark Button -->
      <button class="bookmark-btn" @click="$emit('toggle-bookmark', property.id)">
        {{ property.bookmarked ? '❤️ Saved' : '🤍 Save' }}
      </button>
    </div>

  </div>
</template>

<script>
export default {
  name: 'PropertyCard',
  props: {
    property: {
      type: Object,
      required: true
    }
  },
  emits: ['toggle-bookmark']
}
</script>