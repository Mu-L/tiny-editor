<script setup lang="ts">
import type FluentEditor from '@opentiny/fluent-editor'
import { onMounted } from 'vue'

let editor: FluentEditor
const TOOLBAR_CONFIG = [
  ['ai', { header: [] }],
  ['bold', 'italic', 'underline', 'link'],
  [{ list: 'ordered' }, { list: 'bullet' }],
  ['clean']
]

onMounted(() => {
  // ssr compat, reference: https://vitepress.dev/guide/ssr-compat#importing-in-mounted-hook
  import('@opentiny/fluent-editor').then((module) => {
    const FluentEditor = module.default

    editor = new FluentEditor('#editor-add-toolbar-item', {
      theme: 'snow',
      modules: {
        toolbar: {
          container: TOOLBAR_CONFIG
        },
        ai: {
          host: 'http://localhost:11434',
          model: 'deepseek-r1:8b',
          apiKey: '',
          contentMaxLength: 1000
        }
      }
    })
  })
})
</script>

<template>
  <div id="editor-add-toolbar-item">
    <p>我曾经跨过山和大海，也穿过人山人海</p>
  </div>
</template>
