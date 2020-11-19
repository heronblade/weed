<template>
  <section class="section">
    <div id="top"></div>
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
    <section v-if="loaded">
      <p class="content"><b>Selected:</b> {{ selected }}</p>
      <b-field label="Find a Student">
        <b-autocomplete
          v-model="name"
          rounded
          field="Name"
          :data="filteredDataArray"
          placeholder="e.g. Jimmy Bob"
          icon="magnify"
          clearable
          @select="handleSelect"
        >
          <template slot="empty">No results found</template>
        </b-autocomplete>
      </b-field>
    </section>
    <div class="columns is-mobile chart-wrapper">
      <div
        v-for="item in uploadedFile"
        :key="item.StudentID"
        :class="`chart ${item.StudentID}`"
      >
        <BarChart :data="item"></BarChart>
      </div>
    </div>
    <div class="back-to-top-wrapper">
      <button
        class="back-to-top-link"
        aria-label="Scroll to Top"
        @click="handleBackToTop"
      >
        🔝
      </button>
    </div>
  </section>
</template>

<script>
import BarChart from '@/components/BarChart';

export default {
  name: 'HomePage',
  components: {
    BarChart,
  },
  data() {
    return {
      loaded: false,
      open: true,
      uploadedFile: [],
      name: '',
      selected: null,
    };
  },
  computed: {
    filteredDataArray() {
      return this.uploadedFile.filter((option) => {
        return option.Name.toString()
          .toLowerCase()
          .includes(this.name.toLowerCase());
      });
    },
  },
  methods: {
    handleBackToTop() {
      const top = document.getElementById('top');
      top.scrollIntoView({
        behavior: 'smooth',
        block: 'end',
        inline: 'nearest',
      });
    },
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
        this.loaded = true;
      };
      reader.onload = (e) => {
        that.uploadedFile = JSON.parse(e.target.result);
      };
      reader.readAsText(file);
    },
    handleSelect(option) {
      this.selected = option.Name;
      const elmnt = document.getElementsByClassName(`${option.StudentID}`)[0];
      elmnt.scrollIntoView({
        behavior: 'smooth',
        block: 'end',
        inline: 'nearest',
      });
    },
  },
};
</script>
