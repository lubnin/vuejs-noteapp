<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <message v-if="message" :message="message" />
          <new-note :note="note" @add-note="addNote" />

          <div class="note-header" style="margin: 25px 0">
            <h1>{{ title }}</h1>
            <search
              :value="search"
              placeholder="Find your note"
              @search="search = $event"
            />
            <div class="icons">
              <svg
                :class="{ active: grid }"
                @click="grid = true"
                style="cursor; pointer;"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <rect x="3" y="3" width="7" height="7"></rect>
                <rect x="14" y="3" width="7" height="7"></rect>
                <rect x="14" y="14" width="7" height="7"></rect>
                <rect x="3" y="14" width="7" height="7"></rect>
              </svg>
              <svg
                :class="{ active: !grid }"
                @click="grid = false"
                style="cursor; pointer;"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <line x1="8" y1="6" x2="21" y2="6"></line>
                <line x1="8" y1="12" x2="21" y2="12"></line>
                <line x1="8" y1="18" x2="21" y2="18"></line>
                <line x1="3" y1="6" x2="3" y2="6"></line>
                <line x1="3" y1="12" x2="3" y2="12"></line>
                <line x1="3" y1="18" x2="3" y2="18"></line>
              </svg>
            </div>
          </div>

          <notes :notes="notesFilter" :grid="grid" @remove="removeNote" />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import message from "@/components/Message";
import newNote from "@/components/NewNote";
import notes from "@/components/Notes";
import search from "@/components/Search";

export default {
  components: {
    message,
    newNote,
    notes,
    search,
  },
  data() {
    return {
      title: "Notes App",
      search: "",
      message: null,
      grid: true,
      note: {
        title: "",
        descr: "",
        priority: "standard",
      },
      notes: [
        {
          title: "First Note",
          descr: "Description for first note.",
          priority: "standard",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "Second Note",
          descr: "Description for second note.",
          priority: "standard",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "Third Note",
          descr: "Description for third note.",
          priority: "standard",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "High priority note",
          descr: "I am a very high priority note.",
          priority: "high",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "Low priority note",
          descr: "I am a low priority note.",
          priority: "low",
          date: new Date(Date.now()).toLocaleString(),
        },
      ],
    };
  },
  methods: {
    addNote() {
      if (this.note.title === "") {
        this.message = "title cant be blank!";
        return false;
      }
      if (this.note.priority === "") {
        this.note.priority = "standart";
      }

      let { title, descr, priority } = this.note;
      this.notes.push({
        title,
        descr,
        priority,
        date: new Date().toLocaleString(),
      });
      this.message = null;
      this.note.title = "";
      this.note.descr = "";
      this.note.priority = "standard";
    },
    removeNote(index) {
      this.notes.splice(index, 1);
    },
  },
  computed: {
    notesFilter() {
      let array = this.notes,
        search = this.search;
      if (!search) return array;
      search = search.trim().toLowerCase();
      array = array.filter((item) => {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item;
        }
      });
      return array;
    },
  },
};
</script>

<style lang="scss" scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
