<template>
  <div id="app">
    <DomainPage />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import DomainPage from './Domain/DomainPage.vue'; 

export default defineComponent({
  name: 'App',
  components: {
    DomainPage
  }
});
</script>
