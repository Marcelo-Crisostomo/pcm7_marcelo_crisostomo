<template>
  <div id="HomeView">

    <ListaComponent/>
  </div>
</template>

<script>
// @ is an alias to /src
import ListaComponent from '@/components/ListaComponent.vue';

export default {
  name: 'HomeView',
  components: {
    ListaComponent
  }
}
</script>

<style scoped>

</style>
