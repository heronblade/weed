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
      josh: [
        {
          StudentID: 740447,
          Name: 'Ascher, Brandon F',
          Grade: '09',
          MyAttendance: '60.00',
          AverageAttendanceformyGrade: '97.5',
          AverageAttendanceforaLincolnStudent: '96.2',
        },
        {
          StudentID: 814371,
          Name: 'Beavers, Logan W',
          Grade: '09',
          MyAttendance: '90.0',
          AverageAttendanceformyGrade: '97.5',
          AverageAttendanceforaLincolnStudent: '96.2',
        },
      ],
    };
  },
  mounted() {
    console.log(book);
  },
};
</script>
