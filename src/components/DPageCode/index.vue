<template>
  <div>
    <article class="gitlab" v-if="library === 'gitlab'">
      <div class="file-content code white">
        <div class="line-numbers">
          <template v-for="(line, index) in lines">
            <a class="diff-line-num"
               :data-line-number="line"
               :href="`${$store.state.page.base}#${id}${line}`"
               :id="`${id}${line}`"
               :key="`${index}-l`">
              <i aria-hidden="true" data-hidden="true" class="fa fa-link"></i>
              <span>{{ line }}</span>
            </a>
          </template>
        </div>
        <div class="blob-content"><slot></slot></div>
      </div>
    </article>
    <div v-else class="gist">
      <div class="gist-file">
        <div class="gist-data">
          <div class="js-gist-file-update-container js-task-list-container file-box">
            <div class="file">
              <div itemprop="text" class="blob-wrapper data" v-bind:class="typing">
                <table class="highlight tab-size js-file-line-container" data-tab-size="8">
                  <tbody>
                  <slot></slot>
                  </tbody>
                </table>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DPageCode',

  props: {
    id: {
      type: String,
      default: ''
    },
    library: {
      type: String,
      default: 'github'
    },
    lang: {
      type: String,
      default: 'vue'
    },
    lines: {
      type: Number,
      default: 0
    }
  },

  computed: {
    typing () {
      let type = ''

      switch (this.lang) {
        case 'styl':
          type = 'type-stylus'
          break

        case 'js':
          type = 'type-javascript'
          break

        case 'css':
          type = 'type-css'
          break

        default:
          type = 'type-vue'
      }

      return type
    }
  }
}
</script>

<style lang="stylus"></style>
