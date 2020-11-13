<template>
  <div>
    <p><span id="errorMsg"></span></p>
    <video id="webcam" autoplay="true"/>
    <canvas id="canvas" />
    <div class="controller">
      <button id="snap" playsinline autoplay v-on:click="captureWebcam()">Capture</button>
    </div>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator'
@Component
export default class WebCamFaceAPI extends Vue {
  private constraints = {
    audio: true,
    video: {
      width: 1280, height: 720
    }
  };

  async created () {
    try {
      const stream = await navigator.mediaDevices.getUserMedia(this.constraints)
      this.handleSuccess(stream)
    } catch (e) {
      document.querySelector('span#errorMsg').innerHTML = `navigator.getUserMedia error:${e.toString()}`
    }
  }

  captureWebcam () {
    document.getElementById('canvas').getContext('2d').drawImage(document.getElementById('webcam'), 0, 0, 640, 480)
  }

  // Success
  handleSuccess (stream) {
    window.stream = stream
    document.getElementById('webcam').srcObject = stream
  }
}
</script>
