<template>
  <div class="main-container">
    <h1>Seus Produtos</h1>
    <DashBoard />
  </div>
</template>


<script>
import DashBoard from '@/components/DashBoard.vue';

export default {
    name: "Produtos",
    components: { DashBoard }
}
</script>
