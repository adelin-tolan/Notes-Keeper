<template>
  <div class="notes-container">
    <note-item
      v-for="(note, index) in sortedNotesList"
      :noteTitle="note.noteTitle"
      :noteContent="note.noteContent"
      :noteAuthor="note.noteAuthor"
      :noteDateCreated="dateFormat(note.noteDateCreated)"
      :isHighImportance="note.isHighImportance"
      :keywords="note.keywords"
      :key="index"
    ></note-item>

    <v-btn color="success" dark @click="showHideForm" class="my-6">
      {{ formVisibility ? "Hide form" : "Add note" }}
    </v-btn>

    <add-note-form
      v-if="formVisibility"
      @on-click-add-keyword="addKeyword"
      @on-click-add-node="addNewNote"
      @on-click-reset="resetForm"
    >
    </add-note-form>

    <v-overlay :value="overlay">
      <v-progress-circular indeterminate size="64"></v-progress-circular>
    </v-overlay>
  </div>
</template>

<script>
import NoteItem from "./NoteItem.vue";
import AddNoteForm from "./AddNoteForm.vue";

export default {
  name: "NotesContainer",
  components: {
    NoteItem,
    AddNoteForm,
  },
  data() {
    return {
      notesList: [],
      formVisibility: false,
      noteTitle: "",
      noteContent: "",
      noteAuthor: "",
      isHighImportance: false,
      noteKeyword: "",
      keywords: [],
      overlay: false,
    };
  },
  methods: {
    pad(el) {
      return String(el).padStart(2, 0);
    },
    newDate() {
      const d = new Date();
      return `${d.getFullYear()}-${this.pad(d.getDate())}-${this.pad(
        d.getMonth() + 1
      )}T${this.pad(d.getHours())}:${this.pad(d.getMinutes())}:${this.pad(
        d.getSeconds()
      )}`;
    },

    dateFormat(date) {
      const d = date.split("T");
      const d0 = d[0].split("-");
      return `${d0[1]}/${d0[2]}/${d0[0]}, ${d[1]}`;
    },
    showHideForm() {
      this.formVisibility = !this.formVisibility;
    },
    addKeyword(keyword) {
      this.keywords.push(keyword);
    },

    resetForm() {
      this.noteTitle = "";
      this.noteContent = "";
      this.noteAuthor = "";
      this.isHighImportance = "";
      this.keywords = [];
    },

    addNewNote(title, content, author, isHighImportance, keywordsList) {
      this.notesList.push({
        noteTitle: title || "empty",
        noteContent: content || "empty",
        noteAuthor: author || "empty",
        noteDateCreated: this.newDate(),
        isHighImportance: Boolean(isHighImportance),
        keywords: keywordsList,
      });

      this.resetForm();
    },
  },
  computed: {
    sortedNotesList() {
      const sortedNotesList = [...this.notesList];
      return sortedNotesList.sort(
        (a, b) => b.isHighImportance - a.isHighImportance
      );
    },
  },

  async created() {
    try {
      this.overlay = true;
      const response = await fetch(
        "https://mocki.io/v1/1c2ad75c-6989-4051-9d76-3aceb475d3d2"
      );
      this.notesList = await response.json();
    } catch (err) {
      console.error(err);
    } finally {
      setTimeout(() => {
        this.overlay = false;
      }, 3000);
    }
  },
};
</script>

<style lang="css" scoped></style>
