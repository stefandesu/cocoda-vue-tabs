<template>
  <div class="cocoda-vue-tabs">
    <div class="cocoda-vue-tabs-header">
      <div
        v-for="(tab, index) in tabs"
        :key="`cocoda-vue-tabs-${index}`"
        class="cocoda-vue-tabs-header-item"
        :class="{
          'cocoda-vue-tabs-header-item-active': tab.isActive,
          'cocoda-vue-tabs-header-item-inactive': !tab.isActive,
          'cocoda-vue-tabs-header-item-fill': fill,
        }"
        :style="{
          'flex-basis': fill ? fillMinWidth : 'auto',
          'border-bottom-color': activeColor,
        }"
        @click="activateTab(index)">
        <slot
          :tab="tab"
          :index="index"
          name="title">
          {{ tab.title }}
        </slot>
      </div>
    </div>
    <slot />
  </div>
</template>

<script>
/**
 * Tabs component
 */
export default {
  name: "Tabs",
  props: {
    /**
     * Index of current tab, use with v-model.
     */
    value: {
      type: Number,
      default: null,
    },
    /**
     * Border color for active tab
     */
    activeColor: {
      type: String,
      default: "red",
    },
    /**
     * If true, the tabs will spread over the available space.
     */
    fill: {
      type: Boolean,
      default: false,
    },
    /**
     * Needed if `flex` is true and it is expected that number of tabs will exceed one row.
     */
    fillMinWidth: {
      type: String,
      default: "0",
    },
  },
  data () {
    return {
      activeTab: null,
      activeTabIndex: 0,
      tabs: [],
    }
  },
  computed: {

  },
  watch: {
    tabs(tabs) {
      // Find index of active tab
      let index = tabs.findIndex(tab => this.activeTab == tab)
      index = index == -1 ? (this.value !== null ? this.value : this.activeTabIndex) : index
      this.activateTab(index)
    },
    value(index) {
      this.activateTab(index)
    },
  },
  mounted () {

  },
  methods: {
    registerTab(tab) {
      const index = this.$slots.default.indexOf(tab.$vnode)
      this.tabs.splice(index, 0, tab)
      if (tab.isActive) {
        this.activateTab(index)
      }
    },
    unregisterTab(tab) {
      this.tabs = this.tabs.filter(t => t != tab)
    },
    activateTab (index) {
      if (this.tabs.length > 0) {
        if (index >= this.tabs.length) {
          index = this.tabs.length - 1
        }
        for (let tab of this.tabs) {
          tab.isActive = false
        }
        let tab = this.tabs[index]
        tab.isActive = true
        if (this.activeTab != tab || this.activeTabIndex != index) {
          this.activeTab = tab
          this.activeTabIndex = index
          this.$emit("input", index)
          this.$emit("change", { index, tab })
        }
      }
    },
  },
}
</script>

<style scoped>
.cocoda-vue-tabs {
  display: flex;
  flex-direction: column;
}

/* Fixed header classes */
.cocoda-vue-tabs-header {
  flex: none;
  display: flex;
  flex-wrap: wrap;
  user-select: none;
  margin: 0;
  padding: 0;
  border-bottom: 1px solid rgba(132,141,149,0.2);
  margin-bottom: -1px;
}
.cocoda-vue-tabs-header-item {
  box-sizing: content-box;
  position: relative;
  margin: 0 5px;
  padding: 0 10px;
  height: 32px;
  line-height: 32px;
  border-top: 3px solid transparent;
}
.cocoda-vue-tabs-header-item:first-child {
  margin-left: 0;
}
.cocoda-vue-tabs-header-item:hover {
  cursor: pointer;
}

/* Flexible header classes */
.cocoda-vue-tabs-header-item-inactive {
  padding-bottom: 3px;
  color: #848d95;
}
.cocoda-vue-tabs-header-item-inactive:hover {
  background-color: rgba(132,141,149,0.05);
}
.cocoda-vue-tabs-header-item-active {
  border-bottom: 3px solid transparent;
}
.cocoda-vue-tabs-header-item-active:hover {
  cursor: auto;
}

/* Classes activated by options */
.cocoda-vue-tabs-header-item-fill {
  flex-grow: 1;
  flex-shrink: 1;
  text-align: center;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>
