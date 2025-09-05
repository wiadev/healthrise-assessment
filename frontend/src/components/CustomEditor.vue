<template>
  <div v-if="editor" class="border border-gray-300 rounded-md">
    <div class="border-b border-gray-300">
      <div class="p-1 flex gap-1 flex-wrap">
        <button
          type="button"
          class="p-1.5 text-gray-500 rounded-sm cursor-pointer hover:text-gray-900 hover:bg-gray-100"
          @click="editor.chain().focus().toggleBold().run()"
          :disabled="!editor.can().chain().focus().toggleBold().run()"
          :class="{ 'text-gray-900 bg-gray-100': editor.isActive('bold') }"
        >
          <font-awesome-icon icon="fa-solid fa-bold" />
        </button>
        <button
          type="button"
          class="p-1.5 text-gray-500 rounded-sm cursor-pointer hover:text-gray-900 hover:bg-gray-100"
          @click="editor.chain().focus().toggleItalic().run()"
          :disabled="!editor.can().chain().focus().toggleItalic().run()"
          :class="{ 'text-gray-900 bg-gray-100': editor.isActive('italic') }"
        >
          <font-awesome-icon icon="fa-solid fa-italic" />
        </button>
        <button
          type="button"
          class="p-1.5 text-gray-500 rounded-sm cursor-pointer hover:text-gray-900 hover:bg-gray-100"
          @click="editor.chain().focus().toggleStrike().run()"
          :disabled="!editor.can().chain().focus().toggleStrike().run()"
          :class="{ 'text-gray-900 bg-gray-100': editor.isActive('strike') }"
        >
          <font-awesome-icon icon="fa-solid fa-strikethrough" />
        </button>
        <button
          type="button"
          class="p-1.5 text-gray-500 rounded-sm cursor-pointer hover:text-gray-900 hover:bg-gray-100"
          @click="editor.chain().focus().toggleCode().run()"
          :disabled="!editor.can().chain().focus().toggleCode().run()"
          :class="{ 'text-gray-900 bg-gray-100': editor.isActive('code') }"
        >
          <font-awesome-icon icon="fa-solid fa-code" />
        </button>
        <button
          type="button"
          class="p-1.5 text-gray-500 rounded-sm cursor-pointer hover:text-gray-900 hover:bg-gray-100"
          @click="editor.chain().focus().setParagraph().run()"
          :class="{ 'text-gray-900 bg-gray-100': editor.isActive('paragraph') }"
        >
          <font-awesome-icon icon="fa-solid fa-paragraph" />
        </button>
        <button
          type="button"
          class="p-1.5 text-gray-500 rounded-sm cursor-pointer hover:text-gray-900 hover:bg-gray-100"
          @click="editor.chain().focus().toggleHeading({ level: 1 }).run()"
          :class="{ 'text-gray-900 bg-gray-100': editor.isActive('heading', { level: 1 }) }"
        >
          H1
        </button>
        <button
          type="button"
          class="p-1.5 text-gray-500 rounded-sm cursor-pointer hover:text-gray-900 hover:bg-gray-100"
          @click="editor.chain().focus().toggleHeading({ level: 2 }).run()"
          :class="{ 'text-gray-900 bg-gray-100': editor.isActive('heading', { level: 2 }) }"
        >
          H2
        </button>
        <button
          type="button"
          class="p-1.5 text-gray-500 rounded-sm cursor-pointer hover:text-gray-900 hover:bg-gray-100"
          @click="editor.chain().focus().toggleHeading({ level: 3 }).run()"
          :class="{ 'text-gray-900 bg-gray-100': editor.isActive('heading', { level: 3 }) }"
        >
          H3
        </button>
        <button
          type="button"
          class="p-1.5 text-gray-500 rounded-sm cursor-pointer hover:text-gray-900 hover:bg-gray-100"
          @click="editor.chain().focus().toggleHeading({ level: 4 }).run()"
          :class="{ 'text-gray-900 bg-gray-100': editor.isActive('heading', { level: 4 }) }"
        >
          H4
        </button>
        <button
          type="button"
          class="p-1.5 text-gray-500 rounded-sm cursor-pointer hover:text-gray-900 hover:bg-gray-100"
          @click="editor.chain().focus().toggleHeading({ level: 5 }).run()"
          :class="{ 'text-gray-900 bg-gray-100': editor.isActive('heading', { level: 5 }) }"
        >
          H5
        </button>
        <button
          type="button"
          class="p-1.5 text-gray-500 rounded-sm cursor-pointer hover:text-gray-900 hover:bg-gray-100"
          @click="editor.chain().focus().toggleHeading({ level: 6 }).run()"
          :class="{ 'text-gray-900 bg-gray-100': editor.isActive('heading', { level: 6 }) }"
        >
          H6
        </button>
        <button
          type="button"
          class="p-1.5 text-gray-500 rounded-sm cursor-pointer hover:text-gray-900 hover:bg-gray-100"
          @click="editor.chain().focus().toggleBulletList().run()"
          :class="{ 'text-gray-900 bg-gray-100': editor.isActive('bulletList') }"
        >
          <font-awesome-icon icon="fa-solid fa-list-ul" />
        </button>
        <button
          type="button"
          class="p-1.5 text-gray-500 rounded-sm cursor-pointer hover:text-gray-900 hover:bg-gray-100"
          @click="editor.chain().focus().toggleOrderedList().run()"
          :class="{ 'text-gray-900 bg-gray-100': editor.isActive('orderedList') }"
        >
          <font-awesome-icon icon="fa-solid fa-list-ol" />
        </button>
      </div>
    </div>
    <editor-content :editor="editor" />
  </div>
</template>

<script setup lang="ts">
  import { useEditor, EditorContent } from '@tiptap/vue-3'
  import StarterKit from '@tiptap/starter-kit'
  import { library } from '@fortawesome/fontawesome-svg-core'
  import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
  import { faBold, faItalic, faStrikethrough, faCode, faParagraph, faListUl, faListOl } from '@fortawesome/free-solid-svg-icons'

  library.add(faBold, faItalic, faStrikethrough, faCode, faParagraph, faListUl, faListOl)

  const props = defineProps({
    modelValue: {
      type: String,
      default: '',
    }
  });
  const emit = defineEmits(['update:modelValue']);

  const editor = useEditor({
    content: props.modelValue,
    extensions: [StarterKit],
    onUpdate: ({ editor }) => {
      emit('update:modelValue', editor.getHTML())
    }
  })
  
</script>

<style lang="scss">
/* Basic editor styles */
.tiptap {
  min-height: 100px;
  padding: 4px;
  :first-child {
    margin-top: 0;
  }

  /* List styles */
  ul,
  ol {
    padding: 0 1rem;
    margin: 1.25rem 1rem 1.25rem 0.4rem;

    li p {
      margin-top: 0.25em;
      margin-bottom: 0.25em;
    }
  }

  /* Heading styles */
  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    line-height: 1.1;
    margin-top: 2.5rem;
    text-wrap: pretty;
  }

  h1,
  h2 {
    margin-top: 3.5rem;
    margin-bottom: 1.5rem;
  }

  h1 {
    font-size: 1.4rem;
  }

  h2 {
    font-size: 1.2rem;
  }

  h3 {
    font-size: 1.1rem;
  }

  h4,
  h5,
  h6 {
    font-size: 1rem;
  }

  /* Code and preformatted text styles */
  code {
    background-color: var(--purple-light);
    border-radius: 0.4rem;
    color: var(--black);
    font-size: 0.85rem;
    padding: 0.25em 0.3em;
  }

  pre {
    background: var(--black);
    border-radius: 0.5rem;
    color: var(--white);
    font-family: 'JetBrainsMono', monospace;
    margin: 1.5rem 0;
    padding: 0.75rem 1rem;

    code {
      background: none;
      color: inherit;
      font-size: 0.8rem;
      padding: 0;
    }
  }

  blockquote {
    border-left: 3px solid var(--gray-3);
    margin: 1.5rem 0;
    padding-left: 1rem;
  }

  hr {
    border: none;
    border-top: 1px solid var(--gray-2);
    margin: 2rem 0;
  }
}
</style>