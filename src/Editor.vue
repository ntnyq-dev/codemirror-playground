<script lang="ts" setup>
import { ref, shallowRef } from 'vue'
import { Codemirror } from 'vue-codemirror'
import { javascript } from '@codemirror/lang-javascript'
import { githubLight } from '@uiw/codemirror-theme-github'
import type { EditorView } from '@codemirror/view'
import type { EditorState, Extension } from '@codemirror/state'

interface Payload {
  container: HTMLDivElement
  view: EditorView
  state: EditorState
}

const code = ref(`console.log('Hello, World!')`)
const editorView = shallowRef<EditorView | null>(null)
const extensions = shallowRef<Extension[]>([
  // Languages
  javascript(),
  // Theme
  githubLight,
])

const handleEditorReady = (payload: Payload) => {
  console.log('Editor is ready!', payload)
  editorView.value = payload.view
}
</script>

<template>
  <div class="code-wrapper">
    <Codemirror
      @ready="handleEditorReady"
      v-model="code"
      :style="{ height: '600px' }"
      :tab-size="2"
      :extensions="extensions"
      placeholder="Type some code..."
      autofocus
      indent-with-tab
    />
  </div>
</template>

<style>
.code-wrapper {
  position: relative;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.code-wrapper .v-codemirror {
  position: relative;
  display: block !important;
  width: 80%;
  margin: 0 auto;
}
</style>
