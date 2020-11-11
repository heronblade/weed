<script>
import { Bar } from 'vue-chartjs';

export default {
  extends: Bar,
  props: ['data'],
  mounted() {
    // this.renderChart(this.data);
    this.renderChart(
      {
        labels: ['', 'My Attendance', 'Avg For My Grade', 'Avg for Lincoln'],
        datasets: [
          {
            label: `${this.data.Name} #${this.data.StudentID}`,
            backgroundColor: '#f87979',
            data: [
              0,
              `${this.data.MyAttendance}`,
              `${this.data.AverageAttendanceformyGrade}`,
              `${this.data.AverageAttendanceforaLincolnStudent}`,
            ],
          },
        ],
      },
      {
        responsive: true,
        maintainAspectRatio: false,
      }
    );
  },
};
</script>
