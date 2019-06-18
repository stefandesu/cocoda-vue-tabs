<template>
  <tabs
    size="sm"
    borders>
    <tab title="First Tab">
      Content of first tab
    </tab>
    <tab
      title="Second Tab">
      Content of second tab
    </tab>
    <tab title="Third Tab (longer title)">
      Content of third tab
    </tab>
  </tabs>
</template>

<script>
import Tabs from "./Tabs"
import Tab from "./Tab"

export default {
  name: "Example05",
  components: { Tabs, Tab },
  data () {
    return {}
  },
}
</script>

<style>

</style>
