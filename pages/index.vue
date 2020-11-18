<template>
  <section class="section">
    <div class="columns is-mobile">
      <b-collapse
        class="card file-picker"
        animation="slide"
        aria-id="contentIdForA11y3"
        :open="open"
      >
        <div
          slot="trigger"
          slot-scope="props"
          class="card-header"
          role="button"
          aria-controls="contentIdForA11y3"
        >
          <p class="card-header-title">File Picker</p>
          <a class="card-header-icon">
            <b-icon :icon="props.open ? 'menu-down' : 'menu-up'"> </b-icon>
          </a>
        </div>
        <div class="card-content">
          <div class="content">
            <div class="file-input-wrapper">
              <input type="file" class="file-input" @drop="handleDrop" />
              <p>Drag and Drop your file here</p>
            </div>
          </div>
        </div>
      </b-collapse>
    </div>
    <div class="columns is-mobile chart-wrapper">
      <div v-for="item in uploadedFile" :key="item.StudentID" class="chart">
        <BarChart :data="item"></BarChart>
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
      loaded: false,
      open: true,
      uploadedFile: [],
    };
  },
  methods: {
    handleDrop(event) {
      const that = this;
      event.stopPropagation();
      event.preventDefault();

      const file = event.dataTransfer.files[0];

      const reader = new FileReader();
      reader.onloadstart = () => {
        this.$nuxt.$loading.start();
      };
      reader.onloadend = () => {
        this.$nuxt.$loading.finish();
        this.open = false;
      };
      reader.onload = (e) => {
        that.uploadedFile = JSON.parse(e.target.result);
      };
      reader.readAsText(file);
    },
  },
};
</script>
