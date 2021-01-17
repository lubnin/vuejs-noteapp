.<template>
  <div class="new-note">
    <label>Title</label>
    <input v-model="note.title" type="text" />
    <label>Description</label>
    <textarea v-model="note.descr"></textarea>

    <div class="priorities">
      <p style="text-align: center; margin: 10px 0 2px 10px; font-size: 14px">
        Select note priority:
      </p>

      <div class="priority">
        <label for="low"
          ><input
            type="radio"
            id="low"
            value="low"
            v-model="note.priority"
          />Low</label
        >
      </div>
      <div class="priority">
        <label for="standard"
          ><input
            type="radio"
            id="standard"
            value="standard"
            v-model="note.priority"
          />Standard</label
        >
      </div>
      <div class="priority">
        <label for="high"
          ><input
            type="radio"
            id="high"
            value="high"
            v-model="note.priority"
          />High</label
        >
      </div>
      <br style="clear: both" />
    </div>
    <button class="btn btnPrimary" @click="addNote">New note</button>
  </div>
</template>

<script>
export default {
  props: {
    note: {
      type: Object,
      required: true,
    },
  },
  methods: {
    addNote() {
      this.$emit("add-note", this.note);
    },
  },
};
</script>

<style lang="scss">
.new-note {
  text-align: center;
}
.priorities {
  margin-top: 5px;
  .priority {
    float: left;
  }
  label {
    display: inline-block;
    padding: 0px 2em 0px 5px;
  }
  input {
    display: inline-block;
    width: 25px;
    margin: 5px 0 0 0;
  }
}
</style>