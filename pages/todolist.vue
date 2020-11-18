<template>
  <v-row justify="center" class="todo-container">
    <v-col cols="12">
      <v-card class="todo-wrapper">
        <v-toolbar color="orange" class="todo-toolbar">
          <v-app-bar-nav-icon></v-app-bar-nav-icon>
          <v-toolbar-title class="todo-title">
            <v-text-field
              v-model="todoinput"
              class="todo-textfield"
              value="今週やること"
            ></v-text-field>
            <v-select
              v-model="todoDays"
              class="todo-daysSelect"
              :items="days"
              color="pink"
              label="曜日"
              required
            ></v-select
          ></v-toolbar-title>
          <v-spacer></v-spacer>
          <v-btn icon @click="handleTodoInput()">
            <v-icon>mdi-download</v-icon>
          </v-btn>
        </v-toolbar>
        <v-list>
          <template v-for="(todo, index) in todolists">
            <v-subheader v-if="todo.days" :key="todo.days" inset>
              {{ todo.days }}
            </v-subheader>
            <v-divider v-if="todo.divider" :key="todo" inset> </v-divider>
            <v-list-item
              v-if="todo.work"
              :key="todo.work"
              class="todo-list"
              @click="toggleCheck(index)"
            >
              <v-list-item-avatar v-if="todo.checked === true">
                <v-icon>mdi-check-bold</v-icon>
              </v-list-item-avatar>
              <v-list-item-content>
                <v-list-item-title
                  class="todo-work"
                  v-html="todo.work"
                ></v-list-item-title>
              </v-list-item-content>
              <v-list-item-action>
                <v-icon @click="handleDelete($event, index)"
                  >mdi-window-close</v-icon
                >
              </v-list-item-action>
            </v-list-item>
          </template>
        </v-list>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      todoinput: '',
      todolists: [
        { days: 'Sun', divider: true },
        { work: 'abc', checked: false },
        { days: 'Mon', divider: true },
        { work: 'ghi', checked: true },
        { work: 'ghi', checked: false },
      ],
      days: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sta'],
      todoindex: 2,
    }
  },
  methods: {
    handleTodoInput() {
      if (!this.todoDays) {
        alert('曜日を選択してください。')
        return
      }
      this.todoindex++
      this.todolists.push({
        work: this.todoinput,
        checked: false,
        todoindex: this.todoindex,
      })
      this.todoinput = ''
    },
    toggleCheck(index) {
      this.todolists[index].checked = !this.todolists[index].checked
    },
    handleDelete(e, selectedIndex) {
      e.stopPropagation()
      this.todolists.splice(selectedIndex, 1)
    },
  },
}
</script>
