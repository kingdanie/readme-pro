<template>

  <!--
  This example requires Tailwind CSS v2.0+

  This example requires some changes to your config:

  ```
  // tailwind.config.js
  module.exports = {
    // ...
    plugins: [
      // ...
      require('@tailwindcss/forms'),
    ],
  }
  ```
-->
  <div class="min-h-screen bg-gray-100">
    <!--
      When the mobile menu is open, add `overflow-hidden` to the `body` element to prevent double scrollbars

      Open: "fixed inset-0 z-40 overflow-y-auto", Closed: ""
    -->
    <header class="bg-white shadow-sm lg:static lg:overflow-y-visible">
      <div class="mx-auto q-px-xl">
        <div class="relative flex justify-between lg:gap-8 xl:grid xl:grid-cols-12">
          <div class="flex md:absolute md:inset-y-0 md:left-0 lg:static xl:col-span-2">
            <div class="flex flex-shrink-0 items-center">
              <a href="#">
                <img class="" style="height: 45px;" src="../assets/logo.png" alt=""/>
              </a>
            </div>
          </div>
          <div class="min-w-0 flex-1 md:px-8 lg:px-0 xl:col-span-1">
            <div class="flex items-center px-6 py-4 md:mx-auto md:max-w-3xl lg:mx-0 lg:max-w-none xl:px-0">
              <div class="w-full">
                <label for="search" class="sr-only">Search</label>
                <div class="relative">
                  <div class="pointer-events-none absolute inset-y-0 left-0 flex items-center pl-3 invisible">
                    <!-- Heroicon name: mini/magnifying-glass -->
                    <svg class="h-5 w-5 text-gray-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"
                         fill="currentColor" aria-hidden="true">
                      <path fill-rule="evenodd"
                            d="M9 3.5a5.5 5.5 0 100 11 5.5 5.5 0 000-11zM2 9a7 7 0 1112.452 4.391l3.328 3.329a.75.75 0 11-1.06 1.06l-3.329-3.328A7 7 0 012 9z"
                            clip-rule="evenodd"/>
                    </svg>
                  </div>
                  <input id="search" name="search"
                         class="block invisible w-full rounded-md border border-gray-300 bg-white py-2 pl-10 pr-3 text-sm placeholder-gray-500 focus:border-indigo-500 focus:text-gray-900 focus:placeholder-gray-400 focus:outline-none focus:ring-1 focus:ring-indigo-500 sm:text-sm"
                         placeholder="Search" type="search">
                </div>
              </div>
            </div>
          </div>

          <div class=" lg:flex lg:items-center lg:justify-end xl:col-span-9">

            <!-- Profile dropdown -->
            <div class="border-r-2 q-pr-md cursor-pointer"><a
              class="text-weight-bold text-body1 text-indigo-600 hover:text-indigo-500" target="_blank"
              @click="$router.push({ path: '/github-profile-generator' })" style="text-decoration: none;">
              Github Profile Generator</a></div>
            <div class="border-r-2 q-pl-md q-pr-md "><a
              class="text-weight-bold text-body1 text-indigo-600 hover:text-indigo-500" target="_blank"
              href="https://github.com/mayur091193/readme-pro" style="text-decoration: none;">
              <q-icon name="star" color="yellow-10" size="23px" class="q-mr-xs q-mb-xs"/>
              Star this Repo!</a></div>

            <div class="border-r-2 q-pl-md q-pr-md "><a
              class="text-weight-bold text-body1 text-indigo-600 hover:text-indigo-500" target="_blank"
              href="https://github.com/mayur091193/readme-pro/issues" style="text-decoration: none;">Report Issue</a>
            </div>
            <div class="border-r-2 q-pl-md q-pr-md "><a
              class="text-weight-bold text-body1 text-indigo-600 hover:text-indigo-500" target="_blank"
              href="https://github.com/sponsors/mayur091193" style="text-decoration: none;">Support</a></div>
            <div class="q-pl-md q-pr-md border-r-2"><a target="_blank" href="https://github.com/mayur091193/readme-pro"
                                                       class="text-h6 text-indigo-600 hover:text-indigo-500"
                                                       style="text-decoration: none; "><i aria-hidden="true"
                                                                                          role="presentation"
                                                                                          class="cursor-pointer q-mb-xs fab fa-github q-icon notranslate"
                                                                                          style="font-size: 25px;">
              <!----></i></a></div>

            <div class="rounded-md shadow q-ml-md">
              <a @click="copyMarkdownCode"
                  class="cursor-pointer flex w-full items-center justify-center rounded-md border border-transparent bg-indigo-600 px-4 py-2 text-base text-subtitle2 text-white hover:bg-indigo-700 ">
                <q-icon class="q-mr-sm" name="content_copy"/>
                Copy Markdown</a>
            </div>

          </div>
        </div>
      </div>

    </header>

    <div class="py-6" :style="{'height':available_height}">
      <div class=" lg:grid  lg:grid-cols-12 lg:gap-4 q-pr-xl" :style="{'height':available_height}">
        <div class=" col-span-4 q-pl-xl">
          <div class="sticky top-6 q-pt-sm  bg-white space-y-4 border-2"
               :style="{'height':available_height,'min-height':available_height}" style="overflow-y: auto">
            <!-- Your content -->

            <q-list style="margin-top: 0px;" v-for="(obj_main, index) in all_list_data">
<!--              <q-item-label class="q-py-sm text-indigo-600 text-weight-bold text-subtitle1" header>{{ obj_main.type }}-->
<!--              </q-item-label>-->

              <q-expansion-item
                :default-opened="index==0"
                :label="obj_main.type"
                class="text-indigo-600 text-weight-bold text-subtitle1"
              >
                <q-item class="text-black text-weight-regular" v-for="item in obj_main.children">
                  <q-item-section>
                    <q-item-label>{{ item.label }}</q-item-label>
                  </q-item-section>
                  <q-item-section top side>
                    <div class="text-grey-8 q-gutter-xs">
                      <q-btn v-if="item.label=='Full Profile Template'" class="gt-xs"
                             size="12px" flat dense round icon="info">
                        <q-tooltip
                          transition-show="flip-right"
                          transition-hide="flip-left"
                          class="text-subtitle2"
                        >
                          Just replace your username in the code editor in right.
                        </q-tooltip>
                      </q-btn>
                      <q-btn @click="markdown=markdown + '\n' + item.value" class="gt-xs"
                             size="12px" flat dense round icon="add">
                        <q-tooltip
                          transition-show="flip-right"
                          transition-hide="flip-left"
                        >
                          Add
                        </q-tooltip>
                      </q-btn>
                      <q-btn @click="markdown=item.value" class="gt-xs" size="12px" flat dense
                             round icon="published_with_changes">
                        <q-tooltip
                          transition-show="flip-right"
                          transition-hide="flip-left"
                        >
                          Replace
                        </q-tooltip>
                      </q-btn>
<!--                      <q-btn class="gt-xs" size="12px" flat dense round icon="delete"/>-->
                    </div>
                  </q-item-section>
                </q-item>
              </q-expansion-item>

              <q-separator spaced/>
            </q-list>


          </div>
        </div>

        <div class="col-span-4 border-2" :style="{'height':available_height,'min-height':available_height}">

          <MonacoEditor
            v-if="load_editor"
            theme="vs"
            :options="options"
            language="markdown"
            :diffEditor="false"
            v-model:value="markdown"
          ></MonacoEditor>

        </div>

        <aside class="col-span-4">
          <div class="sticky top-6 space-y-4 border-2 bg-white"
               :style="{'height':available_height,'min-height':available_height}" style="overflow-y: auto">
            <!-- Your content -->
            <q-markdown
              :key="count"
              v-model:src="markdown"
              :no-html="noHtml"
              :no-link="noLink"
              :no-linkify="noLinkify"
              :no-typographer="noTypographer"
              :no-breaks="noBreaks"
              :no-highlight="noHighlight"
              :no-image="noImage"
              :no-container="noContainer"
              :plugins="plugins"
              class=" q-pa-sm "
            />
          </div>
        </aside>

      </div>
    </div>
  </div>


</template>

<style lang="sass">

.q-markdown
  position: relative

  a
    display: inline-block !important

  ul
    display: block
    list-style-type: disc
    margin-top: 1em
    margin-bottom: 1em
    margin-left: 0
    margin-right: 0
    padding-left: 40px

  ol
    display: block
    list-style-type: decimal
    margin-top: 1em
    margin-bottom: 1em
    margin-left: 0
    margin-right: 0
    padding-left: 40px


  code, pre
    font-family: Consolas, Monaco, Andale Mono, Ubuntu Mono, monospace

  pre
    border-radius: $generic-border-radius
    padding: 5px
    margin: 0
    background-size: 1.5em 1.5em
    background-origin: content-box
    background-attachment: local
    max-height: inherit
    height: inherit
    display: block
    overflow: auto
    position: relative
    font-size: 12px
    background: $blue-grey-1
    color: $grey-10
    text-align: left
    white-space: pre
    word-spacing: normal
    word-break: normal
    word-wrap: normal
    line-height: 1.5em
    tab-size: 4
    hyphens: none

  pre code
    border-radius: 0
    width: max-content

  &--heading
    cursor: pointer

    &:after
      content: ' #'
      opacity: 0
      transition: opacity .2s

    &:hover:after
      opacity: 1

    &-h1
      font-size: 2rem
      line-height: 2rem
      padding: 1rem 0
      font-weight: 500
      margin: 0 0 1rem

    &-h2
      font-size: 1.5rem
      line-height: 1.5rem
      padding: 0.5rem 0
      font-weight: 500
      margin: 1rem 0 1rem

    &-h3
      font-size: 1.1rem
      line-height: 1.1rem
      padding: 0.45rem 0
      margin: 1rem 0 1rem

    &-h4
      font-size: 1rem
      line-height: 1rem
      padding: 0.25rem 0
      margin: 1rem 0

    &-h5
      font-size: 0.9rem
      margin: 1rem 0

    &-h6
      font-size: 0.8rem
      margin: 1rem 0

    .q-markdown--link
      border-bottom: inherit
      color: inherit

    &--anchor-link
      cursor: pointer

      &:after
        content: ' #'
        opacity: 0
        transition: opacity .2s

      &:hover:after
        opacity: 1

  &--title-heavy
    border-bottom: 3px solid #ccc

  &--title-light
    border-bottom: 1px solid #ccc

  &--image
    max-width: 100%
    height: auto

  &--link
    font-weight: 500
    text-decoration: none
    outline: 0
    border-bottom: 1px dotted currentColor
    text-align: center
    transition: opacity .2s
    // white-space: nowrap // prevents long headlines from wrapping properly

    &:hover
    // color: yellow

    &-local
      font-family: inherit

    &-external
      font-family: inherit

      &:after
        content: '\e895'
        // hash
        font-family: Material Icons
        font-weight: normal
        font-style: normal
        display: inline-block
        line-height: 1
        text-transform: none
        letter-spacing: normal
        word-wrap: normal
        white-space: nowrap
        direction: ltr
        text-rendering: optimizeLegibility
        -webkit-font-smoothing: antialiased
        -moz-osx-font-smoothing: grayscale
        font-feature-settings: "liga"
        margin: 0 0 0 3px
        padding: 0

  &--token
    white-space: nowrap
    background: $grey-1
    color: $grey-10
    border: $grey-8 solid 1px
    padding: 1px 2px
    font-family: inherit
    border-radius: $generic-border-radius

  &--note
    margin: 14px 0
    padding: 10px
    font-size: 1em
    letter-spacing: .5px
    background: $blue-grey-1
    color: $grey-10
    font-weight: 400

    > p:last-child, .q-markdown--note:last-child
      margin-bottom: 0

    .q-markdown--link
    // color: $grey-2

    &--
      border-left: 10px solid lighten($grey-8, 30%)
      border-radius: 8px 0 0 8px

      .q-markdown--link
        color: lighten($grey-8, 10%)

    &--info
      border-left: 10px solid lighten($blue-8, 30%)
      border-radius: 8px 0 0 8px
      color: $grey-9
      background: $blue-2

      .q-markdown--link
        color: lighten($blue-8, 10%)

      .q-markdown--note-title
        color: lighten($blue-8, 10%)

    &--tip
      border-left: 10px solid lighten($green-8, 30%)
      border-radius: 8px 0 0 8px
      color: $grey-9
      background: $green-2

      .q-markdown--link
        color: lighten($green-8, 10%)

      .q-markdown--note-title
        color: lighten($green-8, 10%)

    &--warning
      border-left: 10px solid lighten($orange-10, 30%)
      border-radius: 8px 0 0 8px
      color: $grey-9
      background: $orange-2

      .q-markdown--link
        color: lighten($orange-10, 10%)

      .q-markdown--note-title
        color: lighten($orange-10, 10%)

    &--danger
      border-left: 10px solid lighten($negative, 30%)
      border-radius: 8px 0 0 8px
      color: $grey-9
      background: $red-2

      .q-markdown--link
        color: lighten($red-8, 10%)

      .q-markdown--note-title
        color: lighten($red-8, 10%)

    &-title
      font-weight: 800
      margin-left: -4px
      margin-right: -4px
      padding: 0 4px
      margin-bottom: 4px

  &--table
    width: fit-content
    margin-bottom: 16px
    border-collapse: collapse
    max-width: 100%
    border-width: 1px
    border-style: solid
    border-color: $grey

  &--line-numbers-wrapper
    display: flex
    justify-content: flex-start
    font-size: 12px
    margin: 0 0 1.0em 0
    background: $blue-grey-1
    color: $grey-10
    font-family: Consolas, Monaco, 'Andale Mono', 'Ubuntu Mono', monospace
    border-radius: $generic-border-radius

  &--line-numbers
    padding: 5px
    text-align: right

  &--line-number
    color: $grey-6
    margin: 0
    position: relative
    text-align: left
    white-space: pre
    word-spacing: normal
    word-break: normal
    word-wrap: normal
    line-height: 1.5
    tab-size: 4
    hyphens: none

  &--code-wrapper
    width: 100%
    min-width: 0

  &--code,
  &--code__inner
    margin: 0
    position: relative
    text-align: left
    white-space: pre
    word-spacing: normal
    word-break: normal
    word-wrap: normal
    line-height: 1.5
    tab-size: 4
    hyphens: none
    border-radius: $generic-border-radius
    background: $blue-grey-1
    color: $grey-10


  &--code
    overflow: visible
    padding: 0

    &__inner
      max-height: inherit
      height: inherit
      display: block
      overflow: auto

  &--table
    border-color: $grey-4
    background: $grey-1

  &--table thead
    background: $grey-4

  &--table thead tr th
    padding: 8px
    border-width: 1px
    border-style: solid
    background: $grey-2

  &--table tbody
    background: $grey-1

  &--table tbody td,
  &--table tbody th
    padding: 8px
    border-width: 1px
    border-style: solid

  &--table tbody tr:nth-child(odd)
    background: $grey-4

// .q-markdown--page > div, .q-markdown--page > pre
//   margin-bottom: 22px

blockquote.q-markdown--link
  background: transparent
  // color: $teal-6

  &:hover
// color: yellow

blockquote.q-markdown--note
  border-width: 1px 8px 1px 8px
  border-radius: 8px
  border-style: solid
  border-color: $grey-6 $teal-6

.q-markdown__copy
  position: absolute
  top: 15px
  right: 15px

.body--dark
  .q-markdown
    color: $grey-2

    code
      background: $grey-9
      color: $grey-2

    .q-markdown--link
      // color: $teal-6

      &:hover
    // color: yellow

    blockquote.q-markdown--note
      border-color: $grey-6 $grey-6
      background: $dark
      color: $grey-2

    pre, pre code
      background: $dark

    .q-markdown--line-numbers-wrapper
      background: $dark
      color: $grey-2

    .q-markdown--token
      background: $grey-6
      color: $grey-10
      border: $grey-4 solid 1px

    .q-markdown--code
      background: $dark
      color: $grey-10

    .q-markdown--note
      background: $grey-10
      color: white
      border-top: 1px solid $grey-9
      border-bottom: 1px solid $grey-9

    .q-markdown--note--
      border-left: 10px solid $grey-6

    .q-markdown--note--info
      border-left: 10px solid $light-blue-10

    .q-markdown--note--tip
      border-left: 10px solid $light-green-10

    .q-markdown--note--warning
      border-left: 10px solid $orange-10

    .q-markdown--note--danger
      border-left: 10px solid $red-10

    .q-markdown--table thead tr th,
    .q-markdown--table tbody
      background-color: $dark

    .q-markdown--table tbody tr:nth-child(2n+1)
      background-color: $grey-9

</style>

<script>
import {defineComponent, ref, watch, onMounted, getCurrentInstance} from 'vue'
import {QMarkdown} from '@quasar/quasar-ui-qmarkdown'
import '@quasar/quasar-ui-qmarkdown/dist/index.css'

import abbreviation from 'markdown-it-abbr'
import deflist from 'markdown-it-deflist'
import emoji from 'markdown-it-emoji'
import footnote from 'markdown-it-footnote'
import insert from 'markdown-it-ins'
import mark from 'markdown-it-mark'
import subscript from 'markdown-it-sub'
import superscript from 'markdown-it-sup'
import taskLists from 'markdown-it-task-lists'
import mermaid from '@datatraccorporation/markdown-it-mermaid'

import MonacoEditor from 'monaco-editor-vue3'

import json_data from '../data/readme_generator_data.js'

import { copyToClipboard } from 'quasar'

export default {
  name: 'Index',
  components: {
    QMarkdown,
    MonacoEditor
  },
  setup() {
    console.log(QMarkdown)
    const
      splitterModel = ref(50),
      markdown = ref('### Select template from left to start...'),
      noHtml = ref(false),
      noLink = ref(false),
      noLinkify = ref(false),
      noTypographer = ref(false),
      noBreaks = ref(false),
      noHighlight = ref(false),
      noEmoji = ref(false),
      noSubscript = ref(false),
      noSuperscript = ref(false),
      noFootnote = ref(false),
      noDeflist = ref(false),
      noAbbreviation = ref(false),
      noInsert = ref(false),
      noMark = ref(false),
      noImage = ref(false),
      noTasklist = ref(false),
      noContainer = ref(false),
      noMermaid = ref(false),
      plugins = ref([]),
      count = ref(0)

    watch([
      noAbbreviation,
      noDeflist,
      noEmoji,
      noFootnote,
      noInsert,
      noMark,
      noSubscript,
      noSuperscript,
      noTasklist,
      noMermaid
    ], () => {
      rebuildPlugins()
    })

    function rebuildPlugins() {
      plugins.value.splice(0, plugins.value.length)

      if (noAbbreviation.value !== true) plugins.value.push(abbreviation)
      if (noDeflist.value !== true) plugins.value.push(deflist)
      if (noEmoji.value !== true) plugins.value.push(emoji)
      if (noFootnote.value !== true) plugins.value.push(footnote)
      if (noInsert.value !== true) plugins.value.push(insert)
      if (noMark.value !== true) plugins.value.push(mark)
      if (noSubscript.value !== true) plugins.value.push(subscript)
      if (noSuperscript.value !== true) plugins.value.push(superscript)
      if (noTasklist.value !== true) plugins.value.push(taskLists)
      if (noMermaid.value !== true) plugins.value.push(mermaid)

      // by having `:key="count"` on the q-markdown component,
      // we can force Vue to do a refresh when the plugins change
      count.value += 1
    }

    onMounted(() => {
      rebuildPlugins()
    })

    return {
      splitterModel,
      markdown,
      noHtml,
      noLink,
      noLinkify,
      noTypographer,
      noBreaks,
      noHighlight,
      noEmoji,
      noSubscript,
      noSuperscript,
      noFootnote,
      noDeflist,
      noAbbreviation,
      noInsert,
      noMark,
      noImage,
      noTasklist,
      noContainer,
      noMermaid,
      plugins,
      count,
      options: ref({
        //Monaco Editor Options
        lineNumbers: 'off',
        minimap: {
          enabled: false
        }
      }),
      load_editor: ref(false),
      available_height: 0,
      all_templates: {
        "github_profile_1": `<p>
  <a href="https://twitter.com/Mayur06322144">
    <img src="https://img.shields.io/twitter/follow/Mayur06322144?label=Follow%20%40Mayur06322144&style=social" alt="Twitter">
  </a>&ensp;
  <a href="https://www.reddit.com/user/mayur091193">
    <img src="https://img.shields.io/reddit/user-karma/combined/mayur091193?style=social" alt="Reddit">
  </a>&ensp;
  <a href="https://stackoverflow.com/users/4762957/mayur-patel?tab=profile">
    <img src="https://img.shields.io/stackexchange/stackoverflow/r/4762957?color=orange" alt="Stackoverflow">
  </a>&ensp;
  <a href="https://dev.to/mayur091193">
    <img src="https://img.shields.io/badge/dev.to-Follow-lightgrey?style=social&logo=dev.to" alt="dev.to">
  </a>
</p>

### Hi there 👋, Mayur here...Thanks for visiting my Profile


- 🔭 I’m currently working on open-source projects (Quasar framework and Vue.js, Angular 12, Python 3.X)
- 🌱 Always learning new Technologies
- 🏗 I’m developing free quasar app extensions, chrome extensions, templates and components
- 💬 Ask me about Quasar framework and Vue.js! And many more technologies like Python-flask framework, JavaScript, jQuery, AngularJS, Angular ...
- 📫 How to reach me: mayur091193@gmail.com
- 💖 Sponsor me to support my open source work. https://github.com/sponsors/mayur091193
- 🌴 Loves nature travel
- 🖼️ Loves to help developers
- 🔗 Owner of q-google-map: https://q-google-map.netlify.app/


---

<div>
  <h4>🏆 Github Profile Trophy</h4>
  <img src="https://github-profile-trophy.vercel.app/?username=mayur091193&column=7"/>
</div>

---

<div>
  <h4>👨🏻‍💻 GitHub Usage stats</h4>
  <img height="170" align="left" src="https://github-readme-stats.vercel.app/api?username=mayur091193&count_private=true&include_all_commits=true" />
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=mayur091193&layout=compact" />
</div>

---
`
      },
      all_items_list: [
        {
          label:'Title and Description',
          value:`
# Title
Description
`
        },
        {
          label:'Support',
          value:`
## Support

If this hepls you in any way, you can contribute to this project by supporting me:

* [💜 Support my open-source work on GitHub](https://github.com/sponsors/mayur091193)

Please check out my sponsor page.

(Every small appreciation can make my day!)

Thank you very much!!
`
        },
        {
          label:'Resources used',
          value:`
## Resources used
* [Quasar Framework](https://quasar.dev/)
* [Vue.js](https://vuejs.org/)
`
        },
        {
          label:'What it deliveres',
          value:`
## What it deliveres
* eCommerce UI template written in Vue.js/Quasar
`
        },
        {
          label:'Future release',
          value:`
## Future release:
* Mobile friendly
* Seller related pages
* Backend(planning to use [Python](https://www.python.org/))
`
        },
        {
          label:'Installation',
          value:`
## Installation

* **Clone the repository**

\`\`\`
git clone https://github.com/mayur091193/quasar-shopping.git
\`\`\`

## Install the dependencies
\`\`\`bash
cd quasar-shopping
npm install
\`\`\`

### To run the app in development mode (hot-code reloading, error reporting, etc.)
\`\`\`bash
quasar dev
\`\`\`


### Build the application
\`\`\`bash
quasar build
\`\`\`
`
        },
        {
          label:'Build',
          value:`
### Build the application
\`\`\`bash
quasar build
\`\`\`
`
        },
        {
          label:'Run',
          value:`
### To run the app in development mode (hot-code reloading, error reporting, etc.)
\`\`\`bash
quasar dev
\`\`\`
`
        },
        {
          label:'Screenshots/UI',
          value:`
**Login option 1**

<p float="left">
        <kbd>
<img src="https://cdn.quasar.dev/img/mountains.jpg" border="1" alt="Alt"
        title="Title"  />
                </kbd>
</p>

**Login option 1**

<p float="left">
        <kbd>
<img src="https://cdn.quasar.dev/img/mountains.jpg" border="1" alt="Alt"
        title="Title"  />
                </kbd>
</p>
`
        },
        {
          label:'License',
          value:`
[MIT](http://opensource.org/licenses/MIT)
`
        }
      ],

      all_list_data :json_data["data"]
    }
  },
  mounted() {
    this.available_height = (window.innerHeight - 105) + 'px';

    this.load_editor = true;

    console.log(this.all_list_data);
  },
  methods: {
    onChange(value) {
      console.log(value);
    },
    getHeight() {
      debugger
      return 800;
    },
    copyMarkdownCode(){
      let self = this;
      copyToClipboard(self.markdown)
      .then(() => {
        self.sendMessage('Markdown Code Copied!')
      })
      .catch(() => {
        // fail
      })

    },
    sendMessage(msg){
      this.$q.notify({
          type: 'positive',
          message: msg,
          position:'bottom-right'
        })
    }
  }
}
</script>
