<template>
  <div class="notes">
    <div
      class="note"
      :class="{ full: !grid }"
      v-for="(note, index) in notes"
      :key="index"
    >
      <div class="note-header" :class="{ full: !grid }">
        <p>{{ note.title }}</p>
        <p style="cursor; pointer;" @click="removeNote(index)">x</p>
      </div>
      <div class="note-body">
        <p :class="note.priority">{{ note.descr }}</p>
        <span>{{ note.date }}</span>
        <span style="float: right">{{ note.priority }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    notes: {
      type: Array,
      required: true,
    },
    grid: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    removeNote(index) {
      this.$emit("remove", index);
    },
  },
};
</script>

<style lang="scss">
.notes {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 40px 0;
}
.note {
  width: 49%;
  padding: 18px 20px;
  margin-bottom: 20px;
  background: #fff;
  transition: all 0.25s cubic-bezier(0.02, 0.01, 0.47, 1);
  box-shadow: 0 30px 30px rgba(0, 0, 0, 0.02);
  &:hover {
    box-shadow: 0 30px 30px rgba(0, 0, 0, 0.04);
    transform: translate(0, -6px);
    transition-delay: 0s !important;
  }
  &.full {
    width: 100%;
    text-align: center;
  }
}

.note-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  h1 {
    font-size: 32px;
  }
  p {
    font-size: 22px;
    color: #2050d4;
  }
  svg {
    margin-right: 12px;
    color: #999999;
    &.active {
      color: #2050d4;
    }
    &:last-child {
      margin-right: 0;
    }
  }
  &.full {
    justify-content: center;
    p {
      margin-right: 16px;
      &:last-child {
        margin-right: 0;
      }
    }
  }
}
.note-body {
  p {
    margin: 20px 0;
    &.high {
      background: #ffdede;
    }
    &.low {
      background: #f6fad7;
    }
  }
  span {
    font-size: 14px;
    color: #999999;
  }
}
</style>