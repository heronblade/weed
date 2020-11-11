<template>
  <section class="section">
    <div class="columns is-mobile chart-wrapper">
      <div v-for="b in book" :key="b.StudentID" class="chart">
        <BarChart :data="b"></BarChart>
      </div>
    </div>
  </section>
</template>

<script>
import BarChart from '@/components/BarChart';
import book from '@/static/book.json';

export default {
  name: 'HomePage',
  components: {
    BarChart,
  },
  data() {
    return {
      book,
    };
  },
};
</script>
