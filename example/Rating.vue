<template>
  <div class="ui rating" :class="[type]"></div>
</template>
<script>
export default {
  props: {
    value: {
      type: Number,
      default: 0,
      required: true
    },
    type: {
      type: String,
      default: "star",
      required: false
    },
    clearable: {
      type: Boolean,
      default: true,
      required: false
    },
    max: {
      type: Number,
      default: 5,
      required: false
    },
    initial: {
      type: Number,
      default: 0,
      required: false
    }
  },

  data() {
    return {
      el: []
    };
  },

  watch: {
    value: function(val, oldVal) {
      if (val === null) {
        this.el[0].rating("clear rating");
      }
    }
  },

  mounted() {
    const t = this;
    t.el = document.getElementsByClassName("ui rating");
    t.el[0].rating({
      initialRating: t.initial,
      maxRating: t.max,
      clearable: t.clearable,
      onRate: function(rating) {
        t.$emit("input", rating);
      }
    });
  }
};
</script>
