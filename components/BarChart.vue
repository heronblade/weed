<script>
import { Bar } from 'vue-chartjs';

export default {
  extends: Bar,
  props: {
    data: {
      type: Object,
      default: () => {},
    },
  },
  mounted() {
    this.renderChart(
      {
        labels: ['', 'My Attendance', 'Avg For My Grade', 'Avg for Lincoln'],
        datasets: [
          {
            label: `${this.data.Name} #${this.data.StudentID} Grade: ${this.data.Grade}`,
            backgroundColor: `#${Math.floor(Math.random() * 16777215).toString(
              16
            )}`,
            data: [
              0,
              `${parseInt(this.data.MyAttendance, 10)}`,
              `${parseInt(this.data.AverageAttendanceformyGrade, 10)}`,
              `${parseInt(this.data.AverageAttendanceforaLincolnStudent, 10)}`,
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
