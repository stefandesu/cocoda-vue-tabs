<template>
  <div>
    <button @click="prependTab">
      Add tab before
    </button>
    <button @click="appendTab">
      Add tab after
    </button>
    Current tab Index: {{ tabIndex }}
    <button @click="jumpToRandom">
      Jump to random tab
    </button>
    <button @click="hiddenTabs.push(tabIndex)">
      Hide current tab
    </button>
    <button @click="hiddenTabs = []">
      Unhide all tab
    </button>
    <tabs
      v-model="tabIndex"
      @change="tabChanged">
      <tab
        v-for="(tab, index) in tabs"
        :key="`example02-${tab}`"
        :hidden="hiddenTabs.includes(index)"
        :title="tab">
        Content of {{ tab }}
      </tab>
      <template v-slot:title="slotProps">
        {{ slotProps.tab.title }}
        <div
          class="closeButton"
          @click="closeTab(slotProps.index)">
          x
        </div>
      </template>
    </tabs>
  </div>
</template>

<script>
import Tabs from "./Tabs"
import Tab from "./Tab"

export default {
  name: "Example02",
  components: { Tabs, Tab },
  data () {
    return {
      tabIndex: 0,
      tabs: ["A tab", "Another tab"],
      hiddenTabs: [],
      tabCount: 0,
    }
  },
  watch: {
    tabs() {
      this.tabCount += 1
    },
  },
  methods: {
    prependTab() {
      this.tabs = [`Tab ${this.tabCount}`].concat(this.tabs)
    },
    appendTab() {
      this.tabs.push(`Tab ${this.tabCount}`)
    },
    jumpToRandom() {
      this.tabIndex = Math.floor(Math.random() * this.tabs.length)
    },
    tabChanged({ index, tab }) {
      console.log("Tab changed to index", index, "with tab", tab)
    },
    closeTab(index) {
      this.tabs.splice(index, 1)
    },
  },
}
</script>

<style>
.closeButton {
  position: absolute;
  top: 0;
  right: 0;
  z-index: 1;
}
.closeButton:hover {
  color: red;
  cursor: pointer;
}
</style>
