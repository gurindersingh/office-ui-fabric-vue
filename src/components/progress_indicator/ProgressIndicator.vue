<template>
  <div class='ms-ProgressIndicator' ref='progressIndicator'>
    <div class='ms-ProgressIndicator-itemName' v-if='name'>{{ name }}</div>
    <div class='ms-ProgressIndicator-itemProgress'>
      <div class='ms-ProgressIndicator-progressTrack'></div>
      <div class='ms-ProgressIndicator-progressBar'></div>
    </div>
    <div class='ms-ProgressIndicator-itemDescription' v-if='description'>{{ description }}</div>
  </div>
</template>
<script>
  export default {
    name: 'ou-progress-indicator',

    props: {
      name: String,
      description: String,

      percent: {
        type: Number,
        validator(value) {
          return value >= 0 && value <= 1;
        }
      }
    },

    data() {
      return {
        progressIndicatorInstance: null
      };
    },

    watch: {
      percent() {
        this.setProgressIndicator();
      }
    },

    mounted() {
      const progressIndicatorElement = this.$refs.progressIndicator;

      this.progressIndicatorInstance = new this.$fabric.ProgressIndicator(progressIndicatorElement);
      this.setProgressIndicator();
    },

    methods: {
      setProgressIndicator() {
        this.progressIndicatorInstance.setProgressPercent(this.percent);
      }
    }
  };
</script>
