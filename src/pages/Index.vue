<template>
  <q-page class="row items-center justify-evenly">
    <WebCamFaceAPI/>
  </q-page>
</template>

<script lang="ts">
import WebCamFaceAPI from 'components/WebCamFaceAPI.vue'
import { Vue, Component } from 'vue-property-decorator'

@Component({
  components: { WebCamFaceAPI }
})
export default class PageIndex extends Vue {
}
</script>
